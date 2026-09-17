# P3__D_balanced__r2

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P3` — Извлечение: карточка товара в JSON (extraction) |
| Пресет | `D_balanced` — D. Сбалансированный (tuned) |
| Параметры | `temperature=0.3, top_k=40, top_p=0.9` |
| Повтор | 2 из 3 |
| Время | 2026-09-14T20:04:57+00:00 |
| Задержка, с | 27.293 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 23.364 |
| Токены (вход/выход) | 284 / 792 |
| из них рассуждения / ответ (оценка) | 718 / 74 |
| Скорость, ток/с | 29.02 (end_to_end) |
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
{
"article": "TK3-220-RU",
"model": "ТЕРМА-К3",
"voltage_v": 220,
"temp_min_c": -25,
"temp_max_c": 60,
"ip_rating": "IP54",
"weight_kg": 1.8,
"manufacturer": "АО «Термоприбор»",
"warranty_months": null,
"price_rub": null
}
```

<details><summary>Блок рассуждений (reasoning)</summary>

```text
*   Role: Business Analyst Assistant.
    *   Language: Russian.
    *   Constraint 1: Strict format (JSON only, no markdown, no intros/outros).
    *   Constraint 2: No extra facts (only from input).
    *   Constraint 3: Handle missing values as `null`.
    *   Input: Product description of "Промышленный контроллер ТЕРМА-К3...".
    *   Required Keys: "article", "model", "voltage_v", "temp_min_c", "temp_max_c", "ip_rating", "weight_kg", "manufacturer", "warranty_months", "price_rub".

    *   "Промышленный контроллер ТЕРМА-К3" -> Model: ТЕРМА-К3
    *   "(артикул TK3-220-RU)" -> Article: TK3-220-RU
    *   "Питание 220 В" -> Voltage: 220
    *   "рабочий диапазон температур от -25 до +60 °C" -> Temp Min: -25, Temp Max: 60
    *   "корпус IP54" -> IP Rating: IP54
    *   "масса 1,8 кг" -> Weight: 1.8
    *   "Производитель — АО «Термоприбор»" -> Manufacturer: АО «Термоприбор»
    *   "Гарантийные обязательства уточняйте у дилера" -> Warranty: null (not specified as a number)
    *   Price: Not mentioned -> null

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

    *   JSON object? Yes.
    *   No markdown? Yes.
    *   No intro/outro? Yes.
    *   No extra facts? Yes.
    *   Russian language? Yes (values).

    ```json
    {
    "article": "TK3-220-RU",
    "model": "ТЕРМА-К3",
    "voltage_v": 220,
    "temp_min_c": -25,
    "temp_max_c": 60,
    "ip_rating": "IP54",
    "weight_kg": 1.8,
    "manufacturer": "АО «Термоприбор»",
    "warranty_months": null,
    "price_rub": null
    }
    ```
```

</details>

## Автопроверки

| Проверка | Балл | Статус | Детали |
| --- | --- | --- | --- |
| схема, значения и null-поля | 1.00 | ✅ | все поля на месте; значения верны; выдуманных значений нет |
| числа не выдуманы | 1.00 | ✅ | все числа есть в исходнике |
| компактный JSON | 1.00 | ✅ | 22 слов (лимит 120) |
| без markdown-обёртки | 1.00 | ✅ | нет: обёртка ``` |
