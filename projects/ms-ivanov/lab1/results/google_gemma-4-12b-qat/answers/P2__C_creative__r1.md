# P2__C_creative__r1

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P2` — Классификация: маршрутизация обращений (classification) |
| Пресет | `C_creative` — C. Креативный (tuned) |
| Параметры | `frequency_penalty=0.3, presence_penalty=0.6, temperature=1.15, top_k=100, top_p=0.97` |
| Повтор | 1 из 3 |
| Время | 2026-09-14T19:55:43+00:00 |
| Задержка, с | 18.899 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 18.026 |
| Токены (вход/выход) | 322 / 546 |
| из них рассуждения / ответ (оценка) | 522 / 24 |
| Скорость, ток/с | 28.89 (end_to_end) |
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
Strictly follow the format (no intros, no apologies), do not add facts not present in the input data.
Classify 6 customer queries into exactly one label from a list: ['Billing', 'Tech support', 'Sales', 'Other'].

        *   If both a technical problem and a request for a plan expansion exist: Choose the label for the *blocking* problem (implied to be the technical issue that prevents progression).
        *   General questions not related to the three main categories: Other.
"number: Label" (6 lines exactly, no headers/explanations).

    1.  *Вчера списали 4 900 ₽ дважды за один и тот же месяц, верните переплату.* (Charged twice for the same month, refund requested.) -> **Billing**
    2.  *После обновления до 2.4.1 приложение падает при открытии отчётов, логи приложил.* (App crashes after update, logs attached.) -> **Tech support**
    3.  *Нас 40 человек, нужна цена на годовую подписку и условия по НДС.* (40 people, want price for annual subscription and VAT conditions.) -> **Sales**
    4.  *Скажите, а ваш офис в Казани работает в субботу?* (Does the Kazan office work on Saturdays?) -> **Other** (General question about location hours).
    5.  *Не приходит счёт-фактура за декабрь, хотя оплата прошла ещё 20-го.* (Invoice for December not received, paid on the 20th.) -> **Billing**
    6.  *Хотим расширить тариф до 100 лицензий, но сначала почините экспорт в Excel — он обрывается.* (Want to expand plan to 100 licenses, but first fix Excel export - it breaks.) -> Both "Sales" (expansion) and "Tech support" (Excel export break). Rule: Choose the blocking problem. A broken feature blocks the upgrade/workflow. Therefore, **Tech support**.

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
