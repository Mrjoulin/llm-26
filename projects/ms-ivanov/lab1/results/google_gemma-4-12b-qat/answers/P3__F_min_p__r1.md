# P3__F_min_p__r1

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P3` — Извлечение: карточка товара в JSON (extraction) |
| Пресет | `F_min_p` — F. Отсечение по min_p (tuned) |
| Параметры | `min_p=0.1, repeat_penalty=1.15, temperature=0.8, top_p=1.0` |
| Повтор | 1 из 3 |
| Время | 2026-09-14T20:07:03+00:00 |
| Задержка, с | 27.128 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 22.694 |
| Токены (вход/выход) | 284 / 758 |
| из них рассуждения / ответ (оценка) | 677 / 81 |
| Скорость, ток/с | 27.94 (end_to_end) |
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
    *   Format requirements: Strict JSON object only (no markdown wrapper), no introductions/apologies.
    *   Constraints: No extra facts, use `null` for missing values, do not infer information.
    *   Required keys: "article", "model", "voltage_v", "temp_min_c", "temp_max_c", "ip_rating", "weight_kg", "manufacturer", "warranty_months", "price_rub".

    *   Description: "Промышленный контроллер ТЕРМА-К3 (артикул TK3-220-RU) предназначен для управления вентиляцией. Питание 220 В, рабочий диапазон температур от -25 до +60 °C, корпус IP54, масса 1,8 кг. Поставляется с креплением на DIN-рейку. Производитель — АО «Термоприбор», сборка в Твери. В комплект входит кабель 1,5 м. Гарантийные обязательства уточняйте у дилера."

    *   "article": "TK3-220-RU"
    *   "model": "ТЕРМА-К3" (or "Терма-К3")
    *   "voltage_v": 220 (extracted from "Питание 220 В")
    *   "temp_min_c": -25 (from "-25 до +60 °C")
    *   "temp_max_c": 60 (from "-25 до +60 °C")
    *   "ip_rating": "IP54"
    *   "weight_kg": 1.8 (from "масса 1,8 кг")
    *   "manufacturer": "АО «Термоприбор»"
    *   "warranty_months": null ("Гарантийные обязательства уточняйте у дилера" -> no specific number)
    *   "price_rub": null (not mentioned)

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

Check constraints: No markdown? Yes. Only JSON? Yes. Russian language (for content)? Yes. Nulls for missing values? Yes. No extra facts? Yes.
```

</details>

## Автопроверки

| Проверка | Балл | Статус | Детали |
| --- | --- | --- | --- |
| схема, значения и null-поля | 1.00 | ✅ | все поля на месте; значения верны; выдуманных значений нет |
| числа не выдуманы | 1.00 | ✅ | все числа есть в исходнике |
| компактный JSON | 1.00 | ✅ | 22 слов (лимит 120) |
| без markdown-обёртки | 1.00 | ✅ | нет: обёртка ``` |
