# P2__A_baseline__r1

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P2` — Классификация: маршрутизация обращений (classification) |
| Пресет | `A_baseline` — A. Базовый (baseline) |
| Параметры | `дефолты движка (ни один параметр не передан)` |
| Повтор | 1 из 3 |
| Время | 2026-09-14T19:53:36+00:00 |
| Задержка, с | 17.404 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 16.543 |
| Токены (вход/выход) | 322 / 479 |
| из них рассуждения / ответ (оценка) | 455 / 24 |
| Скорость, ток/с | 27.52 (end_to_end) |
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
Strictly follow the format, no introductions, no apologies. Do not add facts not present in input.
Classify customer inquiries into exactly one tag from ['Billing', 'Tech support', 'Sales', 'Other'].

        *   If both technical problem and plan expansion: choose the *blocking* problem (usually technical issue prevents action).
        *   General questions not fitting the three categories: Other.
Exactly 6 lines in the format "number: Tag". No explanations, no headers.

    1.  *Вчера списали 4 900 ₽ дважды за один и тот же месяц, верните переплату.* (Double charge, refund request) -> **Billing**.
    2.  *После обновления до 2.4.1 приложение падает при открытии отчётов, логи приложил.* (App crash, technical issue) -> **Tech support**.
    3.  *Нас 40 человек, нужна цена на годовую подписку и условия по НДС.* (Pricing for subscription, VAT conditions) -> **Sales**.
    4.  *Скажите, а ваш офис в Казани работает в субботу?* (Office hours - general info) -> **Other**.
    5.  *Не приходит счёт-фактура за декабрь, хотя оплата прошла ещё 20-го.* (Missing invoice, payment issue) -> **Billing**.
    6.  *Хотим расширить тариф до 100 лицензий, но сначала почините экспорт в Excel — он обрывается.* (Plan expansion + technical issue - export breaks). Rule: blocking problem. Technical problem (export breaks) prevents expansion. -> **Tech support**.

    1: Billing
    2: Tech support
    3: Sales
    4: Other
    5: Billing
    6: Tech support

    *   Russian language? Yes.
    *   Strict format? Yes (6 lines, "number: Tag").
    *   No intros/outros? Yes.
    *   No extra facts? Yes.
```

</details>

## Автопроверки

| Проверка | Балл | Статус | Детали |
| --- | --- | --- | --- |
| точность классификации | 1.00 | ✅ | верно 6/6 |
| разобраны все 6 строк | 1.00 | ✅ | шаблон найден: строка №6 присутствует |
| без лишних пояснений | 1.00 | ✅ | 14 слов (лимит 40) |
