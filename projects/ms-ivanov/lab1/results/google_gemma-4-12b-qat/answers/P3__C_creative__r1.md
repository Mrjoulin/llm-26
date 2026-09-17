# P3__C_creative__r1

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P3` — Извлечение: карточка товара в JSON (extraction) |
| Пресет | `C_creative` — C. Креативный (tuned) |
| Параметры | `frequency_penalty=0.3, presence_penalty=0.6, temperature=1.15, top_k=100, top_p=0.97` |
| Повтор | 1 из 3 |
| Время | 2026-09-14T20:02:58+00:00 |
| Задержка, с | 22.141 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 18.226 |
| Токены (вход/выход) | 284 / 649 |
| из них рассуждения / ответ (оценка) | 575 / 74 |
| Скорость, ток/с | 29.31 (end_to_end) |
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
Assistant to a business analyst.
Russian.
Strictly follow format, no intros, no apologies, no external facts, only JSON object without markdown wrappers.
`article`, `model`, `voltage_v`, `temp_min_c`, `temp_max_c`, `ip_rating`, `weight_kg`, `manufacturer`, `warranty_months`, `price_rub`.

        *   Name: Промышленный контроллер ТЕРМА-К3
        *   Article: TK3-220-RU
        *   Voltage: 220 В
        *   Temp range: -25 to +60 °C
        *   IP rating: IP54
        *   Weight: 1,8 кг
        *   Manufacturer: АО «Термоприбор»
        *   Warranty: "уточняйте у дилера" (Not specified as a number) -> null.
        *   Price: Not mentioned -> null.

    *   "article": "TK3-220-RU"
    *   "model": "ТЕРМА-К3" (or just "КТЕРМА-К3", but usually the name is model). Let's use "ТЕРМА-К3".
    *   "voltage_v": 220
    *   "temp_min_c": -25
    *   "temp_max_c": 60
    *   "ip_rating": "IP54"
    *   "weight_kg": 1.8
    *   "manufacturer": "АО «Термоприбор»"
    *   "warranty_months": null
    *   "price_rub": null

    *   No markdown? Yes.
    *   Only JSON? Yes.
    *   No intros? Yes.

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

</details>

## Автопроверки

| Проверка | Балл | Статус | Детали |
| --- | --- | --- | --- |
| схема, значения и null-поля | 1.00 | ✅ | все поля на месте; значения верны; выдуманных значений нет |
| числа не выдуманы | 1.00 | ✅ | все числа есть в исходнике |
| компактный JSON | 1.00 | ✅ | 22 слов (лимит 120) |
| без markdown-обёртки | 1.00 | ✅ | нет: обёртка ``` |
