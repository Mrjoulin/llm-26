# P2__B_precise__r2

| Поле | Значение |
| --- | --- |
| Модель | `qwen3.5-35b-a3b` |
| Промпт | `P2` — Классификация: маршрутизация обращений (classification) |
| Пресет | `B_precise` — B. Детерминированный (tuned) |
| Параметры | `repeat_penalty=1.05, temperature=0.0, top_k=20, top_p=0.5` |
| Повтор | 2 из 3 |
| Время | 2026-09-14T21:58:17+00:00 |
| Задержка, с | 14.099 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 13.652 |
| Токены (вход/выход) | 316 / 795 |
| из них рассуждения / ответ (оценка) | 771 / 24 |
| Скорость, ток/с | 56.39 (end_to_end) |
| finish_reason | stop |
| Балл качества | 1.0 |

## Промпт

### system

```text
Ты — ассистент бизнес-аналитика. Отвечай на русском языке, строго по формату, без вступлений и извинений. Не добавляй фактов, которых нет во входных данных.
```

### user

```text
Классифицируй обращения клиентов ровно по одной метке из списка: ['Billing', 'Tech support', 'Sales', 'Other'].
Правила: если в обращении есть и техническая проблема, и запрос на расширение тарифа — выбирай метку по блокирующей проблеме. Общие вопросы, не относящиеся к трём категориям, — Other.
Формат ответа: ровно 6 строк вида «номер: Метка». Без пояснений и без заголовков.

1. Вчера списали 4 900 ₽ дважды за один и тот же месяц, верните переплату.
2. После обновления до 2.4.1 приложение падает при открытии отчётов, логи приложил.
3. Нас 40 человек, нужна цена на годовую подписку и условия по НДС.
4. Скажите, а ваш офис в Казани работает в субботу?
5. Не приходит счёт-фактура за декабрь, хотя оплата прошла ещё 20-го.
6. Хотим расширить тариф до 100 лицензий, но сначала почините экспорт в Excel — он обрывается.
```

## Ответ модели

```text
1: Billing
2: Tech support
3: Sales
4: Other
5: Billing
6: Tech support
```

<details><summary>Блок рассуждений (reasoning)</summary>

```text
Thinking Process:

1.  **Analyze the Request:**
    *   Role: Business Analyst Assistant.
    *   Language: Russian.
    *   Constraints: Strict format, no introductions, no apologies, no extra facts not in input.
    *   Task: Classify customer requests into exactly one label from ['Billing', 'Tech support', 'Sales', 'Other'].
    *   Rules:
        *   If both technical issue and tariff expansion request exist -> choose the blocking problem (usually Tech support).
        *   General questions not related to the three main categories -> Other.
    *   Output Format: Exactly 6 lines, format "number: Label". No explanations, no headers.

2.  **Analyze the Input Data:**
    *   Item 1: "Вчера списали 4 900 ₽ дважды за один и тот же месяц, верните переплату." (Double charge, refund request). -> Billing.
    *   Item 2: "После обновления до 2.4.1 приложение падает при открытии отчётов, логи приложил." (App crash after update). -> Tech support.
    *   Item 3: "Нас 40 человек, нужна цена на годовую подписку и условия по НДС." (Price inquiry for subscription). -> Sales.
    *   Item 4: "Скажите, а ваш офис в Казани работает в субботу?" (Office hours/location question). -> Other (not Billing, Tech, or Sales).
    *   Item 5: "Не приходит счёт-фактура за декабрь, хотя оплата прошла ещё 20-го." (Invoice issue after payment). -> Billing.
    *   Item 6: "Хотим расширить тариф до 100 лицензий, но сначала почините экспорт в Excel — он обрывается." (Tariff expansion + Technical issue). Rule: choose blocking problem. Export crashing is a technical issue preventing work. -> Tech support.

3.  **Draft the Output:**
    1: Billing
    2: Tech support
    3: Sales
    4: Other
    5: Billing
    6: Tech support

4.  **Verify Constraints:**
    *   Russian language? Yes.
    *   Strict format (number: Label)? Yes.
    *   Exactly 6 lines? Yes.
    *   No introductions/apologies? Yes.
    *   Labels from list ['Billing', 'Tech support', 'Sales', 'Other']? Yes.
    *   Rule application correct?
        *   1: Billing (Payment issue).
        *   2: Tech support (Crash).
        *   3: Sales (Price inquiry).
        *   4: Other (General info).
        *   5: Billing (Invoice issue).
        *   6: Tech support (Rule: blocking problem takes precedence over sales/expansion request).

5.  **Final Polish:** Ensure no extra whitespace or text.

    1: Billing
    2: Tech support
    3: Sales
    4: Other
    5: Billing
    6: Tech support

    Wait, check the labels exactly as provided in the list: ['Billing', 'Tech support', 'Sales', 'Other'].
    My draft uses these exact strings.

    Check line count: 1, 2, 3, 4, 5, 6. Correct.

    Ready to generate.cs
```

</details>

## Автопроверки

| Проверка | Балл | Статус | Детали |
| --- | --- | --- | --- |
| точность классификации | 1.00 | ✅ | верно 6/6 |
| разобраны все 6 строк | 1.00 | ✅ | шаблон найден: строка №6 присутствует |
| без лишних пояснений | 1.00 | ✅ | 14 слов (лимит 40) |
