# P3__B_precise__r2

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P3` — Извлечение: карточка товара в JSON (extraction) |
| Пресет | `B_precise` — B. Детерминированный (tuned) |
| Параметры | `repeat_penalty=1.05, temperature=0.0, top_k=20, top_p=0.5` |
| Повтор | 2 из 3 |
| Время | 2026-09-14T20:02:08+00:00 |
| Задержка, с | 27.972 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 23.664 |
| Токены (вход/выход) | 284 / 814 |
| из них рассуждения / ответ (оценка) | 733 / 81 |
| Скорость, ток/с | 29.1 (end_to_end) |
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
    *   Constraint 1: Strict format (JSON only).
    *   Constraint 2: No introductions or apologies.
    *   Constraint 3: Do not add facts not in the input.
    *   Input: Product description of "Промышленный контроллер ТЕРМА-К3".
    *   Output keys: "article", "model", "voltage_v", "temp_min_c", "temp_max_c", "ip_rating", "weight_kg", "manufacturer", "warranty_months", "price_rub".

    *   "Промышленный контроллер ТЕРМА-К3": Model = "ТЕРМА-К3" (or "Терма-К3").
    *   "(артикул TK3-220-RU)": Article = "TK3-220-RU".
    *   "Питание 220 В": Voltage_v = 220.
    *   "рабочий диапазон температур от -25 до +60 °C": Temp_min_c = -25, Temp_max_c = 60.
    *   "корпус IP54": IP_rating = "IP54".
    *   "масса 1,8 кг": Weight_kg = 1.8.
    *   "Производитель — АО «Термоприбор»": Manufacturer = "АО «Термоприбор»".
    *   "Гарантийные обязательства уточняйте у дилера": Warranty_months = null (not specified).
    *   Price: Not mentioned in text. Price_rub = null.

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

    *   No markdown? Yes.
    *   No intro/outro? Yes.
    *   Only JSON? Yes.
    *   Russian language? (Values are in Russian where applicable).
```

</details>

## Автопроверки

| Проверка | Балл | Статус | Детали |
| --- | --- | --- | --- |
| схема, значения и null-поля | 1.00 | ✅ | все поля на месте; значения верны; выдуманных значений нет |
| числа не выдуманы | 1.00 | ✅ | все числа есть в исходнике |
| компактный JSON | 1.00 | ✅ | 22 слов (лимит 120) |
| без markdown-обёртки | 1.00 | ✅ | нет: обёртка ``` |
