# P3__A_baseline__r3

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P3` — Извлечение: карточка товара в JSON (extraction) |
| Пресет | `A_baseline` — A. Базовый (baseline) |
| Параметры | `дефолты движка (ни один параметр не передан)` |
| Повтор | 3 из 3 |
| Время | 2026-09-14T20:01:12+00:00 |
| Задержка, с | 25.507 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 21.821 |
| Токены (вход/выход) | 284 / 740 |
| из них рассуждения / ответ (оценка) | 667 / 73 |
| Скорость, ток/с | 29.01 (end_to_end) |
| finish_reason | stop |
| Балл качества | 1.0 |

## Промпт

### system

```text
Ты — ассистент бизнес-аналитика. Отвечай на русском языке, строго по формату, без вступлений и извинений. Не добавляй фактов, которых нет во входных данных.
```

### user

```text
Извлеки данные из описания товара и верни ТОЛЬКО JSON-объект без markdown-обёртки со следующими ключами:
"article", "model", "voltage_v", "temp_min_c", "temp_max_c", "ip_rating", "weight_kg", "manufacturer", "warranty_months", "price_rub".
Если значение в описании отсутствует — поставь null. Ничего не додумывай.

Описание: Промышленный контроллер ТЕРМА-К3 (артикул TK3-220-RU) предназначен для управления вентиляцией. Питание 220 В, рабочий диапазон температур от -25 до +60 °C, корпус IP54, масса 1,8 кг. Поставляется с креплением на DIN-рейку. Производитель — АО «Термоприбор», сборка в Твери. В комплект входит кабель 1,5 м. Гарантийные обязательства уточняйте у дилера.
```

## Ответ модели

```text
{"article": "TK3-220-RU", "model": "ТЕРМА-К3", "voltage_v": 220, "temp_min_c": -25, "temp_max_c": 60, "ip_rating": "IP54", "weight_kg": 1.8, "manufacturer": "АО «Термоприбор»", "warranty_months": null, "price_rub": null}
```

<details><summary>Блок рассуждений (reasoning)</summary>

```text
*   Role: Business Analyst Assistant.
    *   Language: Russian.
    *   Constraint: Strict format, no intros/apologies, no extra facts, no markdown wrapper.
    *   Input: A product description.
    *   Task: Extract specific data into a JSON object.
    *   Keys: "article", "model", "voltage_v", "temp_min_c", "temp_max_c", "ip_rating", "weight_kg", "manufacturer", "warranty_months", "price_rub".
    *   Null handling: If missing, use `null`. No guessing.

    *   "Промышленный контроллер ТЕРМА-К3" -> Model: ТЕРМА-К3
    *   "(артикул TK3-220-RU)" -> Article: TK3-220-RU
    *   "Питание 220 В" -> voltage_v: 220
    *   "рабочий диапазон температур от -25 до +60 °C" -> temp_min_c: -25, temp_max_c: 60
    *   "корпус IP54" -> ip_rating: IP54
    *   "масса 1,8 кг" -> weight_kg: 1.8
    *   "Производитель — АО «Термоприбор»" -> manufacturer: АО «Термоприбор»
    *   "Гарантийные обязательства уточняйте у дилера" -> warranty_months: null (not specified)
    *   "цена" (price_rub) -> Not mentioned -> null

    *   article: "TK3-220-RU"
    *   model: "ТЕРМА-К3"
    *   voltage_v: 220
    *   temp_min_c: -25
    *   temp_max_c: 60
    *   ip_rating: "IP54"
    *   weight_kg: 1.8
    *   manufacturer: "АО «Термоприбор»"
    *   warranty_months: null
    *   price_rub: null

    *   Strict JSON? Yes.
    *   No markdown? Yes.
    *   No intros? Yes.
    *   No extra facts? Yes.

    {"article": "TK3-220-RU", "model": "ТЕРМА-К3", "voltage_v": 220, "temp_min_c": -25, "temp_max_c": 60, "ip_rating": "IP54", "weight_kg": 1.8, "manufacturer": "АО «Термоприбор»", "warranty_months": null, "price_rub": null}
```

</details>

## Автопроверки

| Проверка | Балл | Статус | Детали |
| --- | --- | --- | --- |
| схема, значения и null-поля | 1.00 | ✅ | все поля на месте; значения верны; выдуманных значений нет |
| числа не выдуманы | 1.00 | ✅ | все числа есть в исходнике |
| компактный JSON | 1.00 | ✅ | 22 слов (лимит 120) |
| без markdown-обёртки | 1.00 | ✅ | нет: обёртка ``` |
