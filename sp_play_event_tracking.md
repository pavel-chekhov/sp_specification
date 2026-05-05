# ТЗ для события Play (pre-launch)

## Формат события

```js
dataLayer.push({
  event: "play_events",
  event_data: {
    event_name: "<string>" // маленькие латинские snake_case
  }
})
```

## События

> Номера событий соответствуют номерам из документа **Pre-Launch Playbook**.

### User Journey / Путь пользователя

| Шаг | Что происходит |
| --- | -------------- |
| 1. First Touch | Юзер видит контент у блогера или рекламу. Мессендж: «Scratch Card выдаётся ДО регистрации» |
| 2. Landing Page | Приходит на лендинг. Первое, что видит: Scratch Card — без регистрации, без барьеров. |
| 3. Scratch Card | Скретчит карточку — открывается сумма бонуса ($0.5–$10). Сразу понимает: вот моя награда, надо забрать. |
| 4. Регистрация | Регистрируется через форму (интеграция с API сайта): email + имя. XP начинается не с нуля. |
| 5. Email opt-in | На почту уходит письмо с ссылкой подтверждения. Без клика — XP не начисляется, бонус не выдаётся. |
| 6. Подтверждение ✓ | После клика — XP стартует, бонус зафиксирован, активируется Daily Loop. |
| 7. Faction Select | Выбирает фракцию. XP буст за выбор. |
| 8. Daily Loop | Каждый день: квесты, задания. XP растёт за лайки под активными публикациями. |
| 9. Request Board | Жмёт «хочу купить» → +1 000 XP, заявка видна всем стейкхолдерам. |
| 10. Launch Day | Email с персональной ссылкой магазина. Открывается магазин — получает покупки. |

---

> **Важно:** пуш событий делать не на клики по кнопкам, а на **success** (ответ сервера, где это возможно).

---

### 3. scratch_card

**Смысл:** пользователь стер карточку и увидел сумму бонуса.

```js
dataLayer.push({
  event: "play_events",
  event_data: {
    event_name: "scratch_card"
  }
})
```

---

### 4. registration

**Смысл:** пользователь отправил email (регистрация через форму под карточкой).

```js
dataLayer.push({
  event: "play_events",
  event_data: {
    event_name: "registration"
  }
})
```

---

### 6. email_confirmed

**Смысл:** пользователь подтвердил email (клик по ссылке из письма).

```js
dataLayer.push({
  event: "play_events",
  event_data: {
    event_name: "email_confirmed"
  }
})
```

---

### 7. faction_selected

**Смысл:** пользователь выбрал фракцию / игру.

```js
dataLayer.push({
  event: "play_events",
  event_data: {
    event_name: "faction_selected"
  }
})
```

---

### 9. request_created

**Смысл:** пользователь создал заявку на покупку (Request Board).

```js
dataLayer.push({
  event: "play_events",
  event_data: {
    event_name: "request_created"
  }
})
```
