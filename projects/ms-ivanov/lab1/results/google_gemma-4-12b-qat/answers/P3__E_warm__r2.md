# P3__E_warm__r2

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P3` — Извлечение: карточка товара в JSON (extraction) |
| Пресет | `E_warm` — E. Тёплый (tuned) |
| Параметры | `temperature=0.7, top_k=40, top_p=0.9` |
| Повтор | 2 из 3 |
| Время | 2026-09-14T20:06:09+00:00 |
| Задержка, с | 25.26 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 21.338 |
| Токены (вход/выход) | 284 / 742 |
| из них рассуждения / ответ (оценка) | 668 / 74 |
| Скорость, ток/с | 29.37 (end_to_end) |
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
    *   Constraint 1: Strictly follow the format (JSON only, no markdown).
    *   Constraint 2: No intro/apology.
    *   Constraint 3: Do not add facts not in the input.
    *   Task: Extract specific keys from a product description.
    *   Keys: "article", "model", "voltage_v", "temp_min_c", "temp_max_c", "ip_rating", "weight_kg", "manufacturer", "warranty_months", "price_rub".

    *   Description: "Промышленный контроллер ТЕРМА-К3 (артикул TK3-220-RU) предназначен для управления вентиляцией. Питание 220 В, рабочий диапазон температур от -25 до +60 °C, корпус IP54, масса 1,8 кг. Поставляется с креплением на DIN-рейку. Производитель — АО «Термоприбор», сборка в Твери. В комплект входит кабель 1,5 м. Гарантийные обязательства уточняйте у дилера."

    *   "article": "TK3-220-RU"
    *   "model": "ТЕРМА-К3"
    *   "voltage_v": 220 (extracted from "220 В")
    *   "temp_min_c": -25 (extracted from "-25")
    *   "temp_max_c": 60 (extracted from "+60")
    *   "ip_rating": "IP54"
    *   "weight_kg": 1.8 (extracted from "1,8 кг")
    *   "manufacturer": "АО «Термоприбор»"
    *   "warranty_months": null (Text says "уточняйте у дилера", not a specific number)
    *   "price_rub": null (Not mentioned)

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
    *   Strict JSON? Yes.
    *   No extra facts? Yes.
```

</details>

## Автопроверки

| Проверка | Балл | Статус | Детали |
| --- | --- | --- | --- |
| схема, значения и null-поля | 1.00 | ✅ | все поля на месте; значения верны; выдуманных значений нет |
| числа не выдуманы | 1.00 | ✅ | все числа есть в исходнике |
| компактный JSON | 1.00 | ✅ | 22 слов (лимит 120) |
| без markdown-обёртки | 1.00 | ✅ | нет: обёртка ``` |
