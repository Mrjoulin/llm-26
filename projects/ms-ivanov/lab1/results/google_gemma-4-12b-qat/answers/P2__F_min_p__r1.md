# P2__F_min_p__r1

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P2` — Классификация: маршрутизация обращений (classification) |
| Пресет | `F_min_p` — F. Отсечение по min_p (tuned) |
| Параметры | `min_p=0.1, repeat_penalty=1.15, temperature=0.8, top_p=1.0` |
| Повтор | 1 из 3 |
| Время | 2026-09-14T19:58:58+00:00 |
| Задержка, с | 21.284 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 20.421 |
| Токены (вход/выход) | 322 / 619 |
| из них рассуждения / ответ (оценка) | 595 / 24 |
| Скорость, ток/с | 29.08 (end_to_end) |
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
    *   Constraint 1: Strict format (no intros/apologies).
    *   Constraint 2: No external facts (only use input data).
    *   Task: Classify client inquiries into exactly one of four labels: ['Billing', 'Tech support', 'Sales', 'Other'].
    *   Rules:
        1. If both technical problem and plan expansion request exist -> choose the "blocking" issue (technical problem takes priority/blocks sales). *Wait, let's re-read.* The prompt says "выбирай метку по блокирующей проблеме". Usually, a tech bug blocks a sale or usage.
        2. General questions not in 3 categories = Other.
    *   Output Format: Exactly 6 lines as "number: Label" without headers/explanations.

    1.  *Вчера списали 4 900 ₽ дважды за один и тот же месяц, верните переплату.* (Double charge - Billing) -> **Billing**
    2.  *После обновления до 2.4.1 приложение падает при открытии отчётов, логи приложил.* (App crash/crash logs - Tech support) -> **Tech support**
    3.  *Нас 40 человек, нужна цена на годовую подписку и условия по НДС.* (Price inquiry for subscription - Sales) -> **Sales**
    4.  *Скажите, а ваш офис в Казани работает в субботу?* (Office hours - Other) -> **Other**
    5.  *Не приходит счёт-фактура за декабрь, хотя оплата прошла ещё 20-го.* (Invoice missing after payment - Billing) -> **Billing**
    6.  *Хотим расширить тариф до 100 лицензий, но сначала почините экспорт в Excel — он обрывается.* (Expansion request + Technical bug). Rule: "если в обращении есть и техническая проблема, и запрос на расширение тарифа — выбирай метку по блокирующей проблеме." A technical problem blocks the expansion. -> **Tech support**

    1: Billing
    2: Tech support
    3: Sales
    4: Other
    5: Billing
    6: Tech support

    - Russian language? Yes.
    - Strict format (number: Label)? Yes.
    - No intros/apologies? Yes.
    - Only input data facts? Yes.
    - Exactly 6 lines? Yes.

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
