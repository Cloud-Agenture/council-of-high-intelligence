# Двигун аналізу ринку і пошуку угод — білд-спека

> **Це технічне завдання для агента побудови.** Виконується без уточнень: усі формули, теги, ендпойнти, схеми й приймальні тести — тут.
> Філософія й обмеження — `00-CORE-SPEC.md`. Ліцензійні пастки — `12-SUPERBASE.md` §1. Класи доказів — `13-NO-BROKER-API.md`.
> Мова коду — Python. Мова ідентифікаторів — англійська. Мова коментарів — на розсуд виконавця.

---

## 0. Що будуємо і чого не будуємо

**Будуємо:** конвейєр, який щоночі проходить тисячі інструментів, відсіює до одиниць, і на кожного вижившого видає **меморандум на одну сторінку з доказами й фальсифікаторами** для рішення людини.

**Не будуємо:** прогнозів ціни · автоматичного виконання · «сигналів купівлі» · моделей, що навчаються на власних виходах · чогось, що торкається брокерського API (його немає).

**Три речі, які система дає, і жодна з них — не «краще судження»:**

| | |
|---|---|
| **Покриття** | механічний прохід по всьому всесвіту щоночі, без утоми й вибірковості уваги |
| **Пам'ять** | кожна теза, фальсифікатор і рішення — з поверненням. Люди забувають, **чому** купили |
| **Дисципліна** | переконлива історія не може перестрибнути щабель |

---

## 1. Лійка

```
             ВСЕСВІТ  (~6000 інструментів)
                 │  Щабель 0: доступність, ліквідність, заборони
                 ▼
          ДОПУЩЕНІ  (~2500)
                 │  Щабель 1: СКРИНЕРИ — детерміновано, щоночі
                 ▼
         КАНДИДАТИ  (~20–60/міс)
                 │  Щабель 2: збагачення — детермінований збір + витяг фактів
                 ▼
      ЗБАГАЧЕНІ  (~20–60)
                 │  Щабель 3: теза — LLM, структурований вихід
                 ▼
            ТЕЗИ  (~10–30)
                 │  Щабель 4: опонент — інший провайдер
                 ▼
        ВИЖИВШІ  (~3–10)
                 │  Щабель 5: придатність до портфеля — детерміновано
                 ▼
       МЕМОРАНДУМИ  (~1–5/міс)
                 │
                 ▼
         РІШЕННЯ ЛЮДИНИ
```

**Правило лійки:** відсів на кожному щаблі **логується з причиною**. Через рік має бути можливо спитати «скільки кандидатів убив опонент і за що» — і отримати відповідь.

**Кожен кандидат, що дійшов до щабля 3, реєструється як прогноз** (§9). Це єдиний спосіб дізнатися, які скринери працюють.

---

## 2. Структура репозиторію

```
analysis-engine/
├── contracts/              # JSON Schema — заморожений інтерфейс. Джерело правди
│   ├── sourced_value.schema.json
│   ├── candidate.schema.json
│   ├── thesis.schema.json
│   ├── rebuttal.schema.json
│   └── memo.schema.json
├── ingest/                 # детерміновані фетчери, один модуль на джерело
│   ├── edgar/              # submissions, companyfacts, frames, full-text, forms 4/13F/N-PORT
│   ├── fred.py             # з вінтажами ALFRED
│   ├── treasury.py
│   ├── finra.py
│   └── prices.py           # EODHD
├── store/
│   ├── documents.py        # content-addressed архів: sha256 → blob
│   ├── facts.py            # факти з провенансом
│   └── chain.py            # append-only з prev_hash (див. 13-NO-BROKER-API)
├── screens/                # ОДИН МОДУЛЬ НА СКРИНЕР
│   ├── base.py             # Screen ABC: fire() + base_rate() обов'язкові
│   ├── graham_defensive.py
│   ├── owner_earnings_yield.py
│   ├── insider_cluster.py
│   ├── smart_money_13f.py
│   ├── buyback_plus_insider.py
│   ├── low_with_intact_fundamentals.py
│   ├── special_situations.py
│   └── etf_overlap.py
├── enrich/
│   ├── fundamentals.py
│   ├── news_window.py
│   ├── etf_holdings.py     # N-PORT
│   └── duration.py         # QuantLib
├── agents/                 # ЄДИНЕ МІСЦЕ, ДЕ Є LLM
│   ├── extractor.py        # факт із документа → SourcedValue
│   ├── thesis.py           # структурована теза
│   └── devil.py            # ІНШИЙ ПРОВАЙДЕР. Обов'язково
├── portfolio/
│   ├── theta.py            # ліміт за материнською групою
│   ├── neff.py             # 1/ρ_avg
│   ├── overlap.py          # ваговий перетин
│   └── sizing.py           # ½ Kelly, ≤3.3%
├── registry/               # реєстр прогнозів (див. §9)
├── regime/                 # регулятор «де ми зараз»
├── memo/                   # рендер однієї сторінки
└── tests/
    ├── contracts/          # схеми відхиляють неповне
    ├── screens/            # кожен скринер має тест базової ставки
    ├── determinism/        # двічі запустив — той самий результат
    └── golden/             # зафіксовані очікувані виходи
```

---

## 3. Контракти даних

### 3.1 `SourcedValue` — атом системи

**Жодне число не перетинає межу модуля інакше, ніж у цій обгортці.**

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "SourcedValue",
  "type": "object",
  "required": ["value", "unit", "as_of", "source_url", "retrieved_at",
               "source_sha256", "evidence_class", "method"],
  "additionalProperties": false,
  "properties": {
    "value":         { "type": ["number", "string", "null"] },
    "unit":          { "type": "string", "examples": ["USD", "ratio", "shares", "pct_annual"] },
    "as_of":         { "type": "string", "format": "date",
                       "description": "дата, до якої належить значення" },
    "knowable_from": { "type": "string", "format": "date",
                       "description": "ОБОВ'ЯЗКОВО для бектесту: дата подання документа. Факт не існує до неї" },
    "source_url":    { "type": "string", "format": "uri" },
    "retrieved_at":  { "type": "string", "format": "date-time" },
    "source_sha256": { "type": "string", "pattern": "^[a-f0-9]{64}$",
                       "description": "хеш архівованого тіла документа. Агент не порахує хеш того, чого не завантажив" },
    "evidence_class":{ "enum": ["A", "B"] },
    "method":        { "enum": ["api_fetch", "xbrl_tag", "computed", "document_extraction", "manual"] },
    "computed_by":   { "type": ["string", "null"], "examples": ["quantlib==1.36", "screens.graham_defensive@v3"] },
    "extracted_by":  { "type": ["string", "null"], "description": "model id + версія, лише для document_extraction" }
  }
}
```

**Три поля, які роблять це не декорацією:**

- **`source_sha256`** — витягнути неможливо, не завантаживши документ.
- **`knowable_from`** — дата **подання**, не дата періоду. Без неї будь-який бектест підглядає вперед: звітність за Q1 стає відомою лише в момент подання, а не 31 березня. `companyfacts` віддає `filed` для кожного факту — брати саме його.
- **`evidence_class`** — `A` авторитетне, `B` попереднє (`13-NO-BROKER-API.md` §2.1).

**Тест приймання:** `tests/contracts/test_rejects_unsourced.py` — значення без `source_url`, без `source_sha256` або без `knowable_from` **відхиляється схемою**, не рев'ю. Валідація проти **експортованого JSON Schema**, а не проти Python-класу: контракт має бути артефактом, який можна віддати аудитору.

### 3.2 `Candidate`

```json
{
  "required": ["candidate_id","instrument","fired_screens","created_at","universe_snapshot_sha256"],
  "properties": {
    "candidate_id": {"type":"string"},
    "instrument": {"required":["symbol","figi","cik","asset_class","broker_availability"]},
    "fired_screens": {"type":"array","items":{
        "required":["screen_id","screen_version","fired_at","inputs"],
        "properties":{"inputs":{"type":"array","items":{"$ref":"sourced_value.schema.json"}}}}},
    "rejected_at_stage": {"type":["integer","null"]},
    "rejection_reason":  {"type":["string","null"]}
  }
}
```

### 3.3 `Thesis` — вихід LLM щабля 3

```json
{
  "required": ["candidate_id","must_be_true","value_range","falsifiers",
               "competence_check","whats_in_the_price","outside_view",
               "confidence","model_id","prompt_sha256"],
  "properties": {
    "must_be_true":  {"type":"array","minItems":1,"maxItems":5,"items":{"type":"string"}},
    "value_range":   {"required":["low","base","high","unit","basis"],
                      "description":"ДІАПАЗОН. Точка відхиляється схемою"},
    "falsifiers":    {"type":"array","minItems":3,"maxItems":5,"items":{
                        "required":["event","observable_where","kills_thesis"]}},
    "competence_check": {"required":["in_circle","three_things_understood","what_we_dont_understand"]},
    "whats_in_the_price": {"type":"string","minLength":80,
                      "description":"друге питання Маркса. Теза без цього — не теза"},
    "outside_view":  {"required":["base_rate","base_rate_source","inside_estimate","why_different"]},
    "confidence":    {"required":["p","resolution_date","resolution_criteria"],
                      "properties":{"p":{"type":"number","minimum":0.01,"maximum":0.99}}},
    "prompt_sha256": {"type":"string","pattern":"^[a-f0-9]{64}$"}
  }
}
```

**Чому `p` обмежено 0.01–0.99:** логарифмічна оцінка дає нескінченний штраф при `p=0`. Перший агент, що скаже «впевнений», зламає шлюз.

**Чому `prompt_sha256` обов'язковий:** якість калібрування **сильно залежить від того, як питати**. Незаморожений промпт означає, що 50 прогнозів зроблено 50 різними приладами.

---

## 4. Скринери — ядро пошуку

### 4.1 Обов'язковий контракт

```python
class Screen(ABC):
    screen_id: str
    version: int
    rationale: str          # чому це має працювати — механізм, не «історично працює»

    @abstractmethod
    def fire(self, universe: Universe, as_of: date) -> list[Hit]:
        """Використовує ЛИШЕ факти з knowable_from <= as_of."""

    @abstractmethod
    def base_rate(self) -> BaseRate:
        """ОБОВ'ЯЗКОВО. Скринер без базової ставки — забобон.
        Повертає: частоту спрацювання, розмір вибірки, вікно,
        і що ставалося далі. Порахувано point-in-time."""
```

**Приймальний тест:** `tests/screens/test_every_screen_has_base_rate.py` — рефлексією зібрати всі підкласи `Screen` і впасти, якщо `base_rate()` не реалізовано або повертає порожнє.

**Приймальний тест look-ahead:** `tests/screens/test_no_lookahead.py` — прогнати скринер на `as_of = T`, підсунувши факти з `knowable_from > T`; вихід має бути ідентичним прогону без них.

### 4.2 Акції

Джерело всіх фундаментальних — **EDGAR XBRL**, безкоштовно. Теги us-gaap.

#### `graham_defensive` — Грем, розд. 14

| Умова | Формула | Теги |
|---|---|---|
| Достатній розмір | `Revenues` ≥ порог | `Revenues` або `RevenueFromContractWithCustomerExcludingAssessedTax` |
| Ліквідність ≥2 | `AssetsCurrent / LiabilitiesCurrent ≥ 2` | `AssetsCurrent`, `LiabilitiesCurrent` |
| Борг ≤ робочий капітал | `LongTermDebtNoncurrent ≤ AssetsCurrent − LiabilitiesCurrent` | `LongTermDebtNoncurrent` |
| 10 років прибутку | `NetIncomeLoss > 0` усі 10 років | `NetIncomeLoss` |
| P/E ≤15 за 3-річним | `price / mean(EPS[-3:]) ≤ 15` | `EarningsPerShareDiluted` |
| P/B ≤1.5 **або** P/E×P/B ≤22.5 | `p_e * p_b ≤ 22.5` | `StockholdersEquity` |

#### `owner_earnings_yield` — Баффет, лист 1986

```
owner_earnings = NetIncomeLoss
               + DepreciationDepletionAndAmortization
               − maintenance_capex

maintenance_capex ≈ min(PaymentsToAcquirePropertyPlantAndEquipment,
                        DepreciationDepletionAndAmortization)
```

Спрацьовує при `owner_earnings / market_cap ≥ 0.10` — бар'єр 10% Баффета.

**Обов'язково у виході:** `maintenance_capex` — **оцінка**, тому результат є **діапазоном**. Реалізувати як `low` (капвитрати повністю) і `high` (min з D&A). Точка заборонена схемою.

#### `insider_cluster` — Form 4

```
≥3 різні інсайдери (unique reportingOwnerCik)
· транзакційний код "P" (open-market purchase, не опціони)
· у вікні 30 днів
· сукупна сума ≥ порог
```
Джерело: `submissions` → `form == "4"` → парс XML. Виключати код `A` (нагороди) — це не сигнал.

#### `smart_money_13f`

Кураторський список CIK керуючих у конфігу. Нова або збільшена ≥20% позиція.
**Обмеження в rationale обов'язкове:** 13F подається з лагом **до 45 днів** після кінця кварталу, тільки лонги, без коротких і без деривативів. Це запізнілий, неповний сигнал — і скринер має це говорити прямо.

#### `buyback_plus_insider`
Оголошення викупу (8-K, full-text search) **і** купівля інсайдера у вікні 90 днів. Збіг двох незалежних сигналів капіталовкладення.

#### `low_with_intact_fundamentals` — фільтр падаючого ножа
```
ціна в межах 10% від 52-тижневого мінімуму
AND FCF за 4 квартали > 0
AND debt/equity не зросло >25% рік-до-року
AND немає порушення ковенант у 8-K за 12 міс
```

#### `special_situations` — Грінблат
EDGAR full-text search за формами й фразами: спінофи (Form 10, S-1 зі згадкою spin-off), вилучення з індексів, вихід із банкрутства (8-K Item 1.03/emergence).

### 4.3 ETF

#### `etf_overlap` — головний для нашого портфеля
Джерело — **N-PORT (NPORT-P)**, не сторінки емітентів. Причина: регуляторний календар знімає проблему різних кінців місяця (iShares — торговий, Vanguard — календарний) повністю. `edgartools` уже парсить N-PORT.

```
overlap(A,B) = Σ_i min(w_i^A, w_i^B)     # ваговий перетин
look_through_exposure(issuer) = Σ_f (w_f_portfolio × w_issuer_in_f)
```

Спрацьовує **як попередження**: overlap із наявною позицією >0.30 → фонд не додає диверсифікації.

Решта ETF-метрик: TER проти реальної різниці відстеження · спред і ADV · метод реплікації і контрагент свопу — з **KID/KIID і річного звіту**, це документи, не фід (`enrich/etf_holdings.py` + витягач).

### 4.4 Облігації і золото

Крива й реальні дохідності — Treasury XML + FRED. Дюрація й конвекція — QuantLib:
```
ΔP/P ≈ −D_mod·Δy + ½·C·(Δy)²
```

**Золото — обов'язкове застереження в rationale:** зв'язок ціни з реальними ставками **зламався**: R² ≈ 0.84 на 2005–2021, ~0.03 на 2022–23, ~0.07 з 2024. Скринер, побудований на цьому зв'язку, спирається на мертву регресію. Плюс: інфляційно скоригований максимум 1980 року був перевищений лише у вересні 2025 — **45 років реальної просадки**.

---

## 5. Контракти джерел даних

| Джерело | Ендпойнт | Обмеження — закодувати, не покладатися на дисципліну |
|---|---|---|
| EDGAR XBRL facts | `data.sec.gov/api/xbrl/companyfacts/CIK{cik:010d}.json` | **≤10 req/s глобально**; `User-Agent: "<Org> <email>"` обов'язковий, інакше 403 |
| EDGAR frames | `data.sec.gov/api/xbrl/frames/us-gaap/{tag}/USD/CY{y}Q{q}I.json` | те саме. Це поперечний зріз — основа скринінгу |
| EDGAR submissions | `data.sec.gov/submissions/CIK{cik:010d}.json` | те саме |
| EDGAR full-text | `efts.sec.gov/LATEST/search-index?q=...` | те саме |
| FINRA short interest | `api.finra.org/data/group/otcMarket/name/EquityShortInterest` | двічі на місяць |
| FRED | `api.stlouisfed.org/fred/series/observations` | ~120 req/min. **`realtime_start`/`realtime_end` обов'язкові** |
| Treasury | `home.treasury.gov/...?data=daily_treasury_yield_curve&field_tdr_date_value={year}` | XML |
| Ціни | EODHD | €19.99–99.99/міс |
| Новини | Marketaux | $29/міс, 2500/день |

**Обмежувач швидкості EDGAR — на рівні процесу, а не виклику.** Ліміт 10 req/s **глобальний на організацію**: якщо шардити збір по процесах, кожен думатиме, що вкладається, а сукупно ви отримаєте блок IP на 10 хвилин із продовженням. Реалізувати спільний токен-бакет (файловий лок або Redis), а `User-Agent` брати з конфігу з валідацією на реальний email — не з місця виклику, де хтось напише `test test@test.com` і поставить організацію під порушення.

**FRED — тільки вінтажі.** Використання ревізованих рядів робить історію невідтворюваною і додає підглядування вперед. Ревізії CPI й безробіття суттєві. `realtime_start = as_of` завжди.

**Заборонено як джерело:** `yfinance` у детермінованому тракті — це скрапер недокументованого ендпойнта без SLA, який мовчки міняє методологію коригувань і робить історичну переоцінку невідтворюваною. Для прототипу — так, у тракті рішень — ні.

---

## 6. Агенти — єдине місце з LLM

### 6.1 `extractor` — витяг фактів

**Вхід:** архівований документ (sha256) + перелік потрібних полів.
**Вихід:** масив `SourcedValue` з `method: "document_extraction"`.
**Заборонено:** арифметика. Витягує **як написано**, обчислює Python.

```python
# ОБОВ'ЯЗКОВО
client = instructor.patch(..., max_retries=0)
```
**Причина:** повторний запит при відсутньому `source_url` **навчає модель вигадувати URL**, аби пройти валідатор. Відсутнє поле = жорстка відмова, не перепитування.

### 6.2 `thesis` — побудова тези

Вхід: збагачений кандидат. Вихід: `Thesis` за схемою §3.3.

Тверді правила в системному промпті:
- жодного числа без відповідного `SourcedValue` у вході;
- `value_range` — **діапазон**; точка = відмова схеми;
- **три фальсифікатори мінімум**, кожен зі спостережуваним місцем перевірки;
- ніколи «купувати» / «продавати» / «найкращий у класі» — **ESMA: неявні рекомендації рахуються**, і вирішує подача, а не намір;
- `p` між 0.01 і 0.99.

### 6.3 `devil` — опонент

**Інший провайдер. Не інша модель того самого провайдера.** Причина не стилістична: агенти на спільній базовій моделі мають спільні сліпі зони, і це проявляється як **безпідставна згода**, а не як правильність. `σ_min = σ·√ρ` — незалежно від кількості агентів.

Вузький мандат: **знайти спростувальні докази й відповісти, чому воно дешеве.** Дешевизна завжди має причину; питання лише, чи вона тимчасова.

```json
{ "required": ["candidate_id","verdict","strongest_disconfirming_evidence",
               "why_its_cheap","what_the_thesis_ignores","model_id","provider"],
  "properties": { "verdict": {"enum":["survives","dies","needs_more_evidence"]} } }
```

**Приймальний тест:** `tests/agents/test_devil_different_provider.py` — впасти, якщо `devil.provider == thesis.provider`. **Це не попередження, це падіння збірки.**

---

## 7. Придатність до портфеля — детерміновано

```python
def theta_check(candidate, portfolio) -> Verdict:
    """Агрегація за КІНЦЕВИМ МАТЕРИНСЬКИМ ВЛАСНИКОМ, не за назвою брокера.
    Freedom24 + Freedom Armenia = ОДИН контрагент.
    Непідтверджені збільшення зараховуються, зменшення — ні (I9a)."""

def neff(returns) -> float:
    """N_eff = 1/ρ_avg. Не кількість позицій.
    При ρ=0.6 тисяча акцій диверсифікує ледь краще за п'ять."""

def max_position_size(stop_pct=0.30, risk_pct=0.01) -> float:
    """0.01/0.30 ≈ 3.3% капіталу.
    Виведено зі стопу −30% Принципала. ЄДИНИЙ невигаданий поріг специфікації."""

def half_kelly(mu, sigma, r) -> float:
    """f* = (mu−r)/sigma²; повертає 0.5·f*.
    Подвійний Kelly дає РІВНО НУЛЬ зростання; більше — розорення попри реальну перевагу.
    f* квадратично чутлива до sigma, яку ми ОЦІНЮЄМО."""
```

**Заборонено як рейтинг:** Sharpe, beta, VaR. Причина конкретна: на 56 роках денних даних S&P **одне спостереження дало ~80% ексцесу вибірки**. Коли один день домінує четвертий момент, вибіркова дисперсія не є стабільною оцінкою — а Sharpe і beta на ній побудовані. VaR додатково несубадитивний і мовчить саме про те, де живе розорення.

---

## 8. Регулятор режиму — «де ми зараз»

Не прогноз. Спостережувані, за Марксом:
спреди оцінок проти історії · кредитні умови й якість угод · реальні дохідності · **знак кореляції stock↔bond** · частка кандидатів, що проходить скринери (сам по собі індикатор).

**Єдиний вихід:** `promotion_budget` — **скільки кандидатів система взагалі пропускає на щабель 3 цього місяця.**

Агресивність виставляється **обернено** до того, наскільки охоче ризик несуть інші. Коли за ризик платять мало — лійка звужується автоматично, без чиєїсь волі.

Застереження в коді: у 2022 кореляція stock/Treasury була **≈ +0.65** проти історичних **≈ −0.2**. Знак кореляції — **режимна змінна, а не константа**; хардкодити його не можна.

---

## 9. Реєстр прогнозів — петля навчання

Кожна теза щабля 3 реєструється **автоматично**. Два append-only файли, ~300 рядків:

```
registry.jsonl     {id, created_at, question, resolution_criteria, resolves_at,
                    p, screen_ids, agent_id, model_id, prompt_sha256,
                    baseline_p, prev_hash, hash}
resolutions.jsonl  {forecast_id, resolved_at, outcome, resolver_id,
                    resolver_kind, source_url, prev_hash, hash}
```

**Чотири правила, без яких це самообман:**

1. **`baseline_p` пишеться в тому ж записі, у той самий момент.** Детермінована базова лінія реєструє свою ймовірність одночасно, до того як результат став відомим. Оцінка — `skill = 1 − BS_agent/BS_baseline`.
2. **Жоден агент не розв'язує власний прогноз. Жодна LLM не є єдиним розв'язувачем.** Схемне обмеження, не політика.
3. **Коригування на складність обов'язкове.** Інакше агент, який реєструє лише легкі прогнози, поб'є будь-який абсолютний поріг — і це найімовірніший спосіб зламати шлюз.
4. **Рекалібрування перед оцінюванням заборонено.** Температурне масштабування заявлених ймовірностей «відмиває» погано каліброваного агента у добре каліброваного й нищить сенс шлюзу.

**Перед фіксацією порогу вибірки:** запустити `min_track_record_length()` (Bailey/López de Prado, реалізація в `purgedcv`, MIT). При 50 бінарних прогнозах стандартна помилка Brier біля 0.20 становить ~0.03–0.04 — розрізнити реальну перевагу від удачі майже неможливо. **50 обрано як кругле число; статистика може сказати 200.** Умова допуску: `n ≥ N AND bootstrap_lower_95(skill) > 0`, а не `n ≥ 50 AND skill > 0`.

---

## 10. Приймальні тести — умова «елегантно»

| Тест | Падає, якщо |
|---|---|
`test_rejects_unsourced` | значення без `source_url`/`source_sha256`/`knowable_from` проходить
`test_no_lookahead` | скринер дає інший результат при підсунутих майбутніх фактах
`test_every_screen_has_base_rate` | будь-який `Screen` без `base_rate()`
`test_devil_different_provider` | опонент на тому ж провайдері, що автор тези
`test_determinism` | два прогони на тих самих входах дають різні виходи
`test_no_llm_in_screens` | у `screens/`, `portfolio/`, `enrich/` є виклик моделі
`test_no_vision` | будь-який виклик зору — заборонено повністю (I11)
`test_edgar_rate_limit` | обмежувач не глобальний або `User-Agent` без реального email
`test_fred_vintages` | запит до FRED без `realtime_start`
`test_value_range_not_point` | `value_range` із рівними `low`/`high` без явного обґрунтування
`test_thesis_min_falsifiers` | теза з менш ніж трьома фальсифікаторами
`test_forbidden_ranking_metrics` | Sharpe/beta/VaR використані як рейтинг
`test_golden_memo` | меморандум змінився без зміни версії скринера

---

## 11. Порядок збірки

| Спринт | Що | Готово, коли |
|---|---|---|
| **1** | `contracts/` + `store/` + обмежувач EDGAR | схеми відхиляють неповне; 1000 запитів до EDGAR без 429 |
| **2** | `ingest/edgar` + всесвіт + `graham_defensive` | один скринер працює point-in-time, `base_rate()` порахована |
| **3** | Решта скринерів акцій | кожен із базовою ставкою, тест look-ahead зелений |
| **4** | `enrich/` + `agents/extractor` | усі числа тези мають провенанс; жодного від моделі |
| **5** | `agents/thesis` + `registry/` | теза проходить схему; прогноз реєструється автоматично |
| **6** | `agents/devil` **на іншому провайдері** | тест провайдера зелений |
| **7** | `portfolio/` + `memo/` | меморандум на одну сторінку |
| **8** | `regime/` | `promotion_budget` звужує лійку без ручного втручання |

**Спринт 2 віддає цінність.** Один скринер із чесною базовою ставкою вже дає більше за нуль скринерів із десятьма агентами.

---

## 12. Чого не будувати — і чому

| Не будувати | Причина |
|---|---|
| Дебатну петлю як у TradingAgents | 358 відкритих issue на еталонній реалізації; жодного провенансу на числах; нуль продакшн-історії |
| Донавчання / fine-tuning | сайзинг, ризик розорення, Kelly — закриті формули. Донавчання не дає нічого, чого не дають формула і фід |
| Прогноз ціни | ми готуємось, а не прогнозуємо. Вихід — сценарії з діапазонами |
| Витяг чисел зором | заборонено (`I11`) |
| `mlfinlab`, `backtrader`, `rateslib`, `backtesting.py`, `pypbo`, `OpenBB`, `beancount` | ліцензії — `12-SUPERBASE.md` §1. `pip install mlfinlab` = ліцензійний інцидент |
| `yfinance` у тракті рішень | скрапер без SLA; мовчки міняє коригування |
| Власний XBRL-парсер | `edgartools` (MIT, живий) |

---

## 13. Що виконавець має спитати перед стартом

1. **Всесвіт** — які інструменти доступні на трьох брокерах. Без цього щабель 0 неможливий.
2. **Кураторський список CIK керуючих** для `smart_money_13f`.
3. **Другий провайдер для `devil`** — який саме доступний. Це блокує спринт 6.
4. **Пороги скринерів** — стартові значення з таблиць вище чи інші.
5. **`min_track_record_length`** — запустити й повідомити, скільки прогнозів реально потрібно, **до** фіксації 50.

Усе інше в цьому документі — виконуване як є.
