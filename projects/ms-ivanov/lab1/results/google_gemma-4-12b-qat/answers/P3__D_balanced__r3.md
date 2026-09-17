# P3__D_balanced__r3

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P3` — Извлечение: карточка товара в JSON (extraction) |
| Пресет | `D_balanced` — D. Сбалансированный (tuned) |
| Параметры | `temperature=0.3, top_k=40, top_p=0.9` |
| Повтор | 3 из 3 |
| Время | 2026-09-14T20:05:21+00:00 |
| Задержка, с | 24.477 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 20.572 |
| Токены (вход/выход) | 284 / 714 |
| из них рассуждения / ответ (оценка) | 640 / 74 |
| Скорость, ток/с | 29.17 (end_to_end) |
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
    *   Constraint 3: No extra facts (only from input).
    *   Constraint 4: No markdown wrapping (no ```json ... ```).
    *   Input: Product description of a controller.
    *   Required keys: "article", "model", "voltage_v", "temp_min_c", "temp_max_c", "ip_rating", "weight_kg", "manufacturer", "warranty_months", "price_rub".

    *   Description: "Промышленный контроллер ТЕРМА-К3 (артикул TK3-220-RU) предназначен для управления вентиляцией. Питание 220 В, рабочий диапазон температур от -25 до +60 °C, корпус IP54, масса 1,8 кг. Поставляется с креплением на DIN-рейку. Производитель — АО «Термоприбор», сборка в Твери. В комплект входит кабель 1,5 м. Гарантийные обязательства уточняйте у дилера."

    *   "article": TK3-220-RU
    *   "model": ТЕРМА-К3
    *   "voltage_v": 220
    *   "temp_min_c": -25
    *   "temp_max_c": 60
    *   "ip_rating": IP54
    *   "weight_kg": 1.8
    *   "manufacturer": АО «Термоприбор»
    *   "warranty_months": null (description says "check with dealer")
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

    *   Russian language? Yes.
    *   Strict format? Yes.
    *   No intro/apologies? Yes.
    *   No extra facts? Yes.
    *   No markdown? Yes.
```

</details>

## Автопроверки

| Проверка | Балл | Статус | Детали |
| --- | --- | --- | --- |
| схема, значения и null-поля | 1.00 | ✅ | все поля на месте; значения верны; выдуманных значений нет |
| числа не выдуманы | 1.00 | ✅ | все числа есть в исходнике |
| компактный JSON | 1.00 | ✅ | 22 слов (лимит 120) |
| без markdown-обёртки | 1.00 | ✅ | нет: обёртка ``` |
