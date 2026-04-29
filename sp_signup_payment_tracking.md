# ТЗ для событий Sign Up и Add Payment Info — bloxfit.ai

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
    value: 30.03,
    coupon: "SUMMER_FUN",
    payment_type: "Credit Card",
    items: [
    {
      item_id: "SKU_12345",
      item_name: "Pro",
      coupon: "SUMMER_FUN",
      discount: 2.22,
      index: 0,
      item_brand: "Google",
      item_category: "Apparel",
      item_category2: "Adult",
      item_variant: "green",
      price: 10.01,
      quantity: 3
    }
    ]
  }
});
```

| Параметр | Тип | Обязателен | Описание |
|----------|-----|------------|----------|
| `payment_type` | string | да | Тип платёжного метода |
