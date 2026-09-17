# P2__D_balanced__r3

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P2` — Классификация: маршрутизация обращений (classification) |
| Пресет | `D_balanced` — D. Сбалансированный (tuned) |
| Параметры | `temperature=0.3, top_k=40, top_p=0.9` |
| Повтор | 3 из 3 |
| Время | 2026-09-14T19:57:32+00:00 |
| Задержка, с | 22.805 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 21.933 |
| Токены (вход/выход) | 322 / 652 |
| из них рассуждения / ответ (оценка) | 628 / 24 |
| Скорость, ток/с | 28.59 (end_to_end) |
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
*   Role: Business Analyst Assistant.
    *   Language: Russian.
    *   Constraint 1: Strict format (no intros, no apologies).
    *   Constraint 2: No facts not in input.
    *   Task: Classify 6 customer requests into one of four labels: ['Billing', 'Tech support', 'Sales', 'Other'].
    *   Rule 1: If both tech problem and expansion request exist, choose the blocking problem (Tech support).
    *   Rule 2: General questions not in the three categories = Other.
    *   Output Format: Exactly 6 lines, "number: Label". No explanations, no headers.

    1.  "Вчера списали 4 900 ₽ дважды за один и тот же месяц, верните переплату."
        *   Content: Double charge, refund request.
        *   Category: Billing.

    2.  "После обновления до 2.4.1 приложение падает при открытии отчётов, логи приложил."
        *   Content: App crash, logs provided.
        *   Category: Tech support.

    3.  "Нас 40 человек, нужна цена на годовую подписку и условия по НДС."
        *   Content: Pricing for 40 people, VAT conditions.
        *   Category: Sales.

    4.  "Скажите, а ваш офис в Казани работает в субботу?"
        *   Content: Office hours.
        *   Category: Other (not Billing, Tech support, or Sales).

    5.  "Не приходит счёт-фактура за декабрь, хотя оплата прошла ещё 20-го."
        *   Content: Missing invoice, payment done.
        *   Category: Billing.

    6.  "Хотим расширить тариф до 100 лицензий, но сначала почините экспорт в Excel — он обрывается."
        *   Content: Expansion request (Sales) + Export bug (Tech support).
        *   Rule: Blocking problem (Tech support).
        *   Category: Tech support.

    1: Billing
    2: Tech support
    3: Sales
    4: Other
    5: Billing
    6: Tech support

    1: Billing
    2: Tech support
    3: Sales
    4: Other
    5: Billing
    6: Tech support

    *   Russian language? Yes.
    *   Strict format? Yes.
    *   No intros/apologies? Yes.
    *   No extra facts? Yes.
    *   Exactly 6 lines? Yes.
    *   Correct labels? Yes.

    1: Billing
    2: Tech support
    3: Sales
    4: Other
    5: Billing
    6: Tech support
```

</details>

## Автопроверки

| Проверка | Балл | Статус | Детали |
| --- | --- | --- | --- |
| точность классификации | 1.00 | ✅ | верно 6/6 |
| разобраны все 6 строк | 1.00 | ✅ | шаблон найден: строка №6 присутствует |
| без лишних пояснений | 1.00 | ✅ | 14 слов (лимит 40) |
