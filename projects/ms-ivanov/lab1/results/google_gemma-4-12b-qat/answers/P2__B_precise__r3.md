# P2__B_precise__r3

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P2` — Классификация: маршрутизация обращений (classification) |
| Пресет | `B_precise` — B. Детерминированный (tuned) |
| Параметры | `repeat_penalty=1.05, temperature=0.0, top_k=20, top_p=0.5` |
| Повтор | 3 из 3 |
| Время | 2026-09-14T19:55:24+00:00 |
| Задержка, с | 20.78 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 19.909 |
| Токены (вход/выход) | 322 / 599 |
| из них рассуждения / ответ (оценка) | 575 / 24 |
| Скорость, ток/с | 28.83 (end_to_end) |
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
    *   Constraint 2: No extra facts (only from input).
    *   Task: Classify 6 customer requests into one of four labels: ['Billing', 'Tech support', 'Sales', 'Other'].
    *   Rule 1: If both tech problem and plan expansion exist, choose the blocking problem (usually tech support if it prevents use, but let's look at context). Actually, "blocking problem" usually refers to the technical issue preventing the service from working.
    *   Rule 2: General questions not in the three categories = Other.
    *   Output Format: Exactly 6 lines of "number: Label". No explanations, no headers.

    1.  "Вчера списали 4 900 ₽ дважды за один и тот же месяц, верните переплату." (Double charge, refund request) -> **Billing**
    2.  "После обновления до 2.4.1 приложение падает при открытии отчётов, логи приложил." (App crash, logs provided) -> **Tech support**
    3.  "Нас 40 человек, нужна цена на годовую подписку и условия по НДС." (Price inquiry for subscription, VAT conditions) -> **Sales**
    4.  "Скажите, а ваш офис в Казани работает в субботу?" (Office hours) -> **Other**
    5.  "Не приходит счёт-фактура за декабрь, хотя оплата прошла ещё 20-го." (Missing invoice) -> **Billing**
    6.  "Хотим расширить тариф до 100 лицензий, но сначала почините экспорт в Excel — он обрывается." (Expansion + Tech issue). Rule: "выбирай метку по блокирующей проблеме". The export is broken (tech issue), which blocks the expansion/use. -> **Tech support**

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
    *   Format "number: Label"? Yes.

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
