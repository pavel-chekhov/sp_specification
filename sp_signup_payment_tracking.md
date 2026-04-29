# ТЗ для событий Sign Up, Login, Add Payment Info и Add to Cart

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

| Параметр | Тип    | Обязателен | Описание           |
|----------|--------|------------|--------------------|
| `method` | string | да         | Способ регистрации |

---

### login

**Смысл:** пользователь успешно вошёл в аккаунт (ответ сервера подтвердил аутентификацию).

```js
dataLayer.push({
  event: "login",
  user_id: "<user_id>",
  email: "<email>",
  method: "<Способ входа>" // email, google, facebook, etc.
})
```

| Параметр | Тип    | Обязателен | Описание        |
|----------|--------|------------|-----------------|
| `method` | string | да         | Способ входа    |

---

## ecommerce-события

**Значения `item_id` и `price` по выбранным планам подписки:**

| План | `item_id`       | `item_name` | `price` |
|------|-----------------|-------------|---------|
| Pro  | `pro_monthly`   | `Pro`       | 4.99    |
| Max  | `max_monthly`   | `Max`       | 14.99   |

**Общие параметры ecommerce-объекта** (используются в `add_payment_info` и `add_to_cart`):

| Параметр                | Тип    | Обязателен | Описание                       |
|-------------------------|--------|------------|--------------------------------|
| `currency`              | string | да         | `"USD"`, `"EUR"`, `"GBP"`      |
| `value`                 | number | да         | Цена выбранного плана          |
| `items[].item_id`       | string | да         | Идентификатор плана            |
| `items[].item_name`     | string | да         | Название плана                 |
| `items[].item_category` | string | да         | Всегда `"subscription"`        |
| `items[].price`         | number | да         | Цена плана                     |
| `items[].quantity`      | number | да         | Всегда `1`                     |

---

### add_to_cart

**Смысл:** пользователь выбрал вариант подписки, кликнув на кнопку перехода к вводу платежных данных.

```js
dataLayer.push({ ecommerce: null, user_id: "<user_id>" });  // Clear the previous ecommerce object and set user_id

dataLayer.push({
  event: "add_to_cart",
  ecommerce: {
    currency: "<string>",  // "USD" | "EUR" | "GBP"
    value: 4.99,           // цена выбранного плана
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

---

### add_payment_info

**Смысл:** пользователь успешно добавил платёжные данные (ответ платёжного провайдера подтвердил сохранение).

```js
dataLayer.push({ ecommerce: null, user_id: "<user_id>" });  // Clear the previous ecommerce object and set user_id

dataLayer.push({
  event: "add_payment_info",
  ecommerce: {
    currency: "<string>",  // "USD" | "EUR" | "GBP"
    value: 4.99,           // цена выбранного плана
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

**Дополнительный параметр:**

| Параметр       | Тип    | Обязателен | Описание              |
|----------------|--------|------------|-----------------------|
| `payment_type` | string | да         | Тип платёжного метода |


