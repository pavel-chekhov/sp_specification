# ТЗ для события Quest Festival (event tracking)

## Формат события

```js
dataLayer.push({
  event: "quest_festival_events",
  event_data: {
    event_name: "<string>" // маленькие латинские snake_case
  }
})
```

## События

---

### 2. drawer_shown

**Смысл:** пользователь зашёл в приложение — язычок шторки фестиваля отображён на экране.

```js
dataLayer.push({
  event: "quest_festival_events",
  event_data: {
    event_name: "drawer_shown"
  }
})
```

---

### 3. drawer_opened

**Смысл:** пользователь раскрыл шторку фестиваля (потянул язычок или нажал на него).

```js
dataLayer.push({
  event: "quest_festival_events",
  event_data: {
    event_name: "drawer_opened"
  }
})
```

