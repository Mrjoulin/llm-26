# P2__A_baseline__r3

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P2` — Классификация: маршрутизация обращений (classification) |
| Пресет | `A_baseline` — A. Базовый (baseline) |
| Параметры | `дефолты движка (ни один параметр не передан)` |
| Повтор | 3 из 3 |
| Время | 2026-09-14T19:54:21+00:00 |
| Задержка, с | 23.693 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 22.822 |
| Токены (вход/выход) | 322 / 686 |
| из них рассуждения / ответ (оценка) | 662 / 24 |
| Скорость, ток/с | 28.95 (end_to_end) |
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
    *   Constraint 1: Strict format, no introductions, no apologies.
    *   Constraint 2: Do not add facts not in input.
    *   Constraint 3: Classify requests into one of ['Billing', 'Tech support', 'Sales', 'Other'].
    *   Constraint 4: Rule for dual issues (tech + sales) -> choose the "blocking problem" (usually technical if it prevents action, but here the prompt says "choose by blocking problem", let's look at the examples. Usually, a bug is blocking a sale or use).
    *   Constraint 5: General questions not in the 3 categories -> 'Other'.
    *   Constraint 6: Format: Exactly 6 lines "number: Label". No explanations, no headers.

    1. "Вчера списали 4 900 ₽ дважды за один и тот же месяц, верните переплату."
        *   Content: Double payment/refund request.
        *   Category: Billing.
    2. "После обновления до 2.4.1 приложение падает при открытии отчётов, логи приложил."
        *   Content: App crashes, logs provided.
        *   Category: Tech support.
    3. "Нас 40 человек, нужна цена на годовую подписку и условия по НДС."
        *   Content: Pricing for 40 people, VAT conditions.
        *   Category: Sales.
    4. "Скажите, а ваш офис в Казани работает в субботу?"
        *   Content: Office hours.
        *   Category: Other.
    5. "Не приходит счёт-фактура за декабрь, хотя оплата прошла ещё 20-го."
        *   Content: Missing invoice, payment completed.
        *   Category: Billing.
    6. "Хотим расширить тариф до 100 лицензий, но сначала почините экспорт в Excel — он обрывается."
        *   Content: Expand license (Sales) + Fix Excel export (Tech support).
        *   Rule: "choose label by blocking problem". The bug (Excel export) is blocking the action/satisfaction.
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
    *   Strict format (number: Label)? Yes.
    *   No intro/outro? Yes.
    *   No extra facts? Yes.
    *   Exactly 6 lines? Yes.

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
