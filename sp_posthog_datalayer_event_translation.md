# Техническое задание: трансляция PostHog-событий в dataLayer

## Цель

Реализовать подход к трансляции событий, отправляемых в PostHog, в другие аналитические системы через `dataLayer`.

## Задача

События, которые отправляются в PostHog, должны также пушиться в `window.dataLayer`.

Все должно проходить через единую обертку для событий.

## Структура dataLayer-события

```js
window.dataLayer.push({
  event: "posthog_event",
  event_data: {
    name: "<имя события>",
    properties: {}
  }
})
```

Где:

- `event` — фиксированное значение `"posthog_event"`;
- `event_data.name` — имя события, которое отправляется в PostHog;
- `event_data.properties` — свойства события, которые отправляются в PostHog.
