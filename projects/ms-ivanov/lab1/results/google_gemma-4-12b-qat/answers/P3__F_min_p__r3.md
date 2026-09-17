# P3__F_min_p__r3

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P3` — Извлечение: карточка товара в JSON (extraction) |
| Пресет | `F_min_p` — F. Отсечение по min_p (tuned) |
| Параметры | `min_p=0.1, repeat_penalty=1.15, temperature=0.8, top_p=1.0` |
| Повтор | 3 из 3 |
| Время | 2026-09-14T20:08:09+00:00 |
| Задержка, с | 38.839 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 34.422 |
| Токены (вход/выход) | 284 / 1088 |
| из них рассуждения / ответ (оценка) | 1007 / 81 |
| Скорость, ток/с | 28.01 (end_to_end) |
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
    *   Language: Russian (output).
    *   Constraint 1: Strict format (JSON only), no introductions/apologies.
    *   Constraint 2: No extra facts from outside the input data.
    *   Task: Extract specific fields from a product description into JSON.

    *   Input Description: "Промышленный контроллер ТЕРМА-К3 (артикул TK3-220-RU) предназначен для управления вентиляцией. Питание 220 В, рабочий диапазон температур от -25 до +60 °C, корпус IP54, масса 1,8 кг. Поставляется с креплением на DIN-рейку. Производитель — АО «Термоприбор», сборка в Твери. В комплект входит кабель 1,5 м. Гарантийные обязательства уточняйте у дилера."
    *   Required Keys: "article", "model", "voltage_v", "temp_min_c", "temp_max_c", "ip_rating", "weight_kg", "manufacturer", "warranty_months", "price_rub".

    *   `article`: TK3-220-RU
    *   `model`: ТЕРМА-К3
    *   `voltage_v`: 220 (extracted from 220 В)
    *   `temp_min_c`: -25
    *   `temp_max_c`: +60 (or 60, usually numbers are better for JSON unless specified otherwise. I'll keep the sign if it exists but check consistency). Let's use integers where possible or strings if necessary. Usually, numeric values in these contexts are best as numbers/strings depending on format preference. The prompt doesn't specify types, just "values".
    *   `ip_rating`: IP54
    *   `weight_kg`: 1,8 (Note: In Russian text it is a comma. JSON standard usually uses dots for floats, but if I keep the string or convert to float? Usually best to follow common sense for numeric data in JSON - "1.8"). Wait, prompt says "don't add facts".
    *   `manufacturer`: АО «Термоприбор»
    *   `warranty_months`: null (description says "уточняйте у дилера")
    *   `price_rub`: null

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

    *   Strict JSON? Yes.
    *   No markdown wrapper? The prompt says "без markdown-обёртки". This means no \`\`\`json ... \`\`\`. Just raw text.
    *   Russian language used for keys/values where appropriate (keys are fixed).
    *   No extra facts? Yes.

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

    *Self-correction on weight*: The text says "1,8 кг". In JSON numbers use a dot as decimal separator. Since the prompt asks to extract data and not add facts/hallucinate, I should ensure 1.8 is correct or keep it as string if unsure about type conversion. Usually, numeric fields are preferred as floats.

    *Wait*, "без markdown-обёртки" means strictly raw text output starting with `{`.
```

</details>

## Автопроверки

| Проверка | Балл | Статус | Детали |
| --- | --- | --- | --- |
| схема, значения и null-поля | 1.00 | ✅ | все поля на месте; значения верны; выдуманных значений нет |
| числа не выдуманы | 1.00 | ✅ | все числа есть в исходнике |
| компактный JSON | 1.00 | ✅ | 22 слов (лимит 120) |
| без markdown-обёртки | 1.00 | ✅ | нет: обёртка ``` |
