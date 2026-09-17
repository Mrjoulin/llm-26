# P2__F_min_p__r2

| Поле | Значение |
| --- | --- |
| Модель | `google/gemma-4-12b-qat` |
| Промпт | `P2` — Классификация: маршрутизация обращений (classification) |
| Пресет | `F_min_p` — F. Отсечение по min_p (tuned) |
| Параметры | `min_p=0.1, repeat_penalty=1.15, temperature=0.8, top_p=1.0` |
| Повтор | 2 из 3 |
| Время | 2026-09-14T19:59:14+00:00 |
| Задержка, с | 16.076 |
| TTFT (первый токен), с | — |
| До начала ответа, с | 15.219 |
| Токены (вход/выход) | 322 / 466 |
| из них рассуждения / ответ (оценка) | 442 / 24 |
| Скорость, ток/с | 28.99 (end_to_end) |
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

        *   Classify client requests into exactly one label from: ['Billing', 'Tech support', 'Sales', 'Other'].
        *   Rule 1 (Priority): If both a technical problem and an upgrade request exist, choose the *blocking problem*. (Usually "Tech support" is blocking for sales/upgrades).
        *   Rule 2 (General questions): Use 'Other'.
Exactly 6 lines in format "number: Label". No intro, no apologies, no extra facts.

    1.  "Вчера списали 4 900 ₽ дважды за один и тот же месяц, верните переплату." -> Topic: Overpayment/Payment issue. Category: **Billing**.
    2.  "После обновления до 2.4.1 приложение падает при открытии отчётов, логи приложил." -> Topic: App crash/Technical bug. Category: **Tech support**.
    3.  "Нас 40 человек, нужна цена на годовую подписку и условия по НДС." -> Topic: Pricing inquiry for new subscription. Category: **Sales**.
    4.  "Скажите, а ваш офис в Казани работает в субботу?" -> Topic: Office hours (not Billing, Tech support, or Sales). Category: **Other**.
    5.  "Не приходит счёт-фактура за декабрь, хотя оплата прошла ещё 20-го." -> Topic: Invoice missing/Payment issue. Category: **Billing**.
    6.  "Хотим расширить тариф до 100 лицензий, но сначала почините экспорт в Excel — он обрывается." -> Topics: Upgrade (Sales) + Bug in export (Tech support). Rule applies: Choose blocking problem. A bug that prevents usage/export is a technical blocker for the upgrade. Category: **Tech support**.

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
