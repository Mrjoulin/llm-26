# P2__C_creative__r2

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P2` — Классификация: маршрутизация обращений (classification) |
| Пресет | `C_creative` — C. Креативный (tuned) |
| Параметры | `frequency_penalty=0.3, presence_penalty=0.6, temperature=1.15, top_k=100, top_p=0.97` |
| Повтор | 2 из 3 |
| Время | 2026-09-14T19:56:02+00:00 |
| Задержка, с | 19.69 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 18.815 |
| Токены (вход/выход) | 322 / 562 |
| из них рассуждения / ответ (оценка) | 538 / 24 |
| Скорость, ток/с | 28.54 (end_to_end) |
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
Business Analyst Assistant.
Russian.
Strictly according to the format, no introductions, no apologies, no facts outside the input data.
Classify 6 customer inquiries into one of four labels: ['Billing', 'Tech support', 'Sales', 'Other'].

        *   If both technical issue AND request for plan expansion exist $\rightarrow$ choose the label for the *blocking* problem (technical issue usually blocks sales/expansion).
        *   General questions not fitting the 3 main categories $\rightarrow$ 'Other'.
Exactly 6 lines in the format "number: Label". No explanations, no headers.

    1.  *Вчера списали 4 900 ₽ дважды за один и тот же месяц, верните переплату.*
        *   Content: Double payment/refund request.
        *   Category: Billing.
    2.  *После обновления до 2.4.1 приложение падает при открытии отчётов, логи приложил.*
        *   Content: App crash, version info, logs attached.
        *   Category: Tech support.
    3.  *Нас 40 человек, нужна цена на годовую подписку и условия по НДС.*
        *   Content: Pricing for subscription, VAT conditions.
        *   Category: Sales.
    4.  *Скажите, а ваш офис в Казани работает в субботу?*
        *   Content: Office hours/location. (Not Billing, Tech support, or Sales).
        *   Category: Other.
    5.  *Не приходит счёт-фактура за декабрь, хотя оплата прошла ещё 20-го.*
        *   Content: Invoice missing, payment status.
        *   Category: Billing.
    6.  *Хотим расширить тариф до 100 лицензий, но сначала почините экспорт в Excel — он обрывается.*
        *   Content: Expansion (Sales) + Technical issue (Export breaking).
        *   Rule application: "Technical problem and expansion request -> choose blocking problem". A broken export blocks the usage/expansion process.
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
```

</details>

## Автопроверки

| Проверка | Балл | Статус | Детали |
| --- | --- | --- | --- |
| точность классификации | 1.00 | ✅ | верно 6/6 |
| разобраны все 6 строк | 1.00 | ✅ | шаблон найден: строка №6 присутствует |
| без лишних пояснений | 1.00 | ✅ | 14 слов (лимит 40) |
