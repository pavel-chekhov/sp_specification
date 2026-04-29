# ТЗ для событий Sign Up и Add Payment Info

---

> **Важно:** пуш событий делать не на клики по кнопкам, а на **success** (ответ сервера, где это возможно).

---

## События

### sign_up

**Смысл:** пользователь успешно завершил регистрацию (ответ сервера подтвердил создание аккаунта).

```js
dataLayer.push({
  event: "sign_up",
  user_id: "<user_id>",
  email: "<email>",
  method: "<Способ регистрации>" // email, google, facebook, etc.
})
```

| Параметр | Тип | Обязателен | Описание |
|----------|-----|------------|----------|
| `method` | string | да | Способ регистрации |

---

### add_payment_info

**Смысл:** пользователь успешно добавил платёжные данные (ответ платёжного провайдера подтвердил сохранение).

```js
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "add_payment_info",
  ecommerce: {
    currency: "USD",
    value: 4.99,          // цена выбранного плана
    payment_type: "<string>", // "Credit Card" | "PayPal" | etc.
    items: [
      {
        item_id: "<string>",       // "pro_monthly" | "max_monthly"
        item_name: "<string>",     // "Pro" | "Max"
        item_category: "subscription",
        price: 4.99,               // цена выбранного плана
        quantity: 1
      }
    ]
  }
});
```

**Значения `item_id` и `price` по планам:**

| План | `item_id`       | `price` |
|------|-----------------|---------|
| Pro  | `pro_monthly`   | `4.99`  |
| Max  | `max_monthly`   | `14.99` |

**Все параметры события:**

| Параметр                | Тип    | Обязателен | Описание                       |
|-------------------------|--------|------------|--------------------------------|
| `currency`              | string | да         | Валюта — всегда `"USD"`        |
| `value`                 | number | да         | Цена выбранного плана          |
| `payment_type`          | string | да         | Тип платёжного метода          |
| `items[].item_id`       | string | да         | Идентификатор плана            |
| `items[].item_name`     | string | да         | Название плана                 |
| `items[].item_category` | string | да         | Всегда `"subscription"`        |
| `items[].price`         | number | да         | Цена плана                     |
| `items[].quantity`      | number | да         | Всегда `1`                     |
