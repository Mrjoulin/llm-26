# P2__F_min_p__r3

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P2` — Классификация: маршрутизация обращений (classification) |
| Пресет | `F_min_p` — F. Отсечение по min_p (tuned) |
| Параметры | `min_p=0.1, repeat_penalty=1.15, temperature=0.8, top_p=1.0` |
| Повтор | 3 из 3 |
| Время | 2026-09-14T19:59:35+00:00 |
| Задержка, с | 20.873 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 20.009 |
| Токены (вход/выход) | 322 / 605 |
| из них рассуждения / ответ (оценка) | 581 / 24 |
| Скорость, ток/с | 28.98 (end_to_end) |
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
    *   Constraints: Strict format, no intros/apologies, no external facts, strictly follow the provided classification rules and labels.
    *   Labels: ['Billing', 'Tech support', 'Sales', 'Other'].
    *   Rule 1 (Priority): If both tech issue + expansion request -> choose blocking problem (tech).
    *   Rule 2 (Default): General questions not in categories -> Other.
    *   Output Format: Exactly 6 lines, "number: Label". No explanations or headers.

    *   Item 1: "Вчера списали 4 900 ₽ дважды за один и тот же месяц, верните переплату." (Charged twice for the same month, refund needed).
        *   Category: Billing.
    *   Item 2: "После обновления до 2.4.1 приложение падает при открытии отчётов, логи приложил." (App crashes on report opening after update, logs attached).
        *   Category: Tech support.
    *   Item 3: "Нас 40 человек, нужна цена на годовую подписку и условия по НДС." (Need price for annual subscription and VAT conditions).
        *   Category: Sales.
    *   Item 4: "Скажите, а ваш офис в Казани работает в субботу?" (Does the Kazan office work on Saturday?).
        *   Category: Other (General question).
    *   Item 5: "Не приходит счёт-фактура за декабрь, хотя оплата прошла ещё 20-го." (Invoice for December not received despite payment).
        *   Category: Billing.
    *   Item 6: "Хотим расширить тариф до 100 лицензий, но сначала почините экспорт в Excel — он обрывается." (Want to expand license count but fix the broken Excel export first).
        *   Analysis: Contains both expansion request ("расширить тариф") and technical problem ("экспорт... обрывается").
        *   Rule application: Choose blocking problem. "Почините" (fix) implies Tech support is the blocker for Sales action.
        *   Category: Tech support.

    1: Billing
    2: Tech support
    3: Sales
    4: Other
    5: Billing
    6: Tech support

    Format check: "number: Label". 6 lines. No headers/intros.

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
