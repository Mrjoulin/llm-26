# P2__E_warm__r3

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P2` — Классификация: маршрутизация обращений (classification) |
| Пресет | `E_warm` — E. Тёплый (tuned) |
| Параметры | `temperature=0.7, top_k=40, top_p=0.9` |
| Повтор | 3 из 3 |
| Время | 2026-09-14T19:58:37+00:00 |
| Задержка, с | 20.241 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 19.38 |
| Токены (вход/выход) | 322 / 580 |
| из них рассуждения / ответ (оценка) | 556 / 24 |
| Скорость, ток/с | 28.65 (end_to_end) |
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
    *   Constraint 2: No outside facts.
    *   Task: Classify 6 customer requests into one of ['Billing', 'Tech support', 'Sales', 'Other'].
    *   Rule 1: If both tech issue and expansion request exist, pick the blocking issue (usually tech support).
    *   Rule 2: General questions not in the three categories are 'Other'.
    *   Format: 6 lines of "number: Label".

    1.  "Вчера списали 4 900 ₽ дважды за один и тот же месяц, верните переплату."
        *   Context: Double payment, refund request.
        *   Category: Billing.

    2.  "После обновления до 2.4.1 приложение падает при открытии отчётов, логи приложил."
        *   Context: App crash, logs provided.
        *   Category: Tech support.

    3.  "Нас 40 человек, нужна цена на годовую подписку и условия по НДС."
        *   Context: Pricing request for a group, VAT conditions.
        *   Category: Sales.

    4.  "Скажите, а ваш офис в Казани работает в субботу?"
        *   Context: Office hours.
        *   Category: Other.

    5.  "Не приходит счёт-фактура за декабрь, хотя оплата прошла ещё 20-го."
        *   Context: Missing invoice, payment status.
        *   Category: Billing.

    6.  "Хотим расширить тариф до 100 лицензий, но сначала почините экспорт в Excel — он обрывается."
        *   Context: Expansion request (Sales) + Tech issue (Tech support).
        *   Rule: Blocking issue (Tech support).
        *   Category: Tech support.

    1: Billing
    2: Tech support
    3: Sales
    4: Other
    5: Billing
    6: Tech support

    *   6 lines? Yes.
    *   Format "number: Label"? Yes.
    *   No intro/outro? Yes.
    *   Russian language? Yes.

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
