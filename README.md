# 🍳 Ma_Gooderz-Meal Timer

A multi-dish cooking timer for Android — queue up everything you're making, start each dish whenever it hits the pan, and get notified before (and when) it's ready. Built to solve a real kitchen problem: juggling several dishes with different cook times without losing track of any of them.

## The problem

Cooking a full meal usually means multiple dishes finishing at different times. It's easy to lose track of what's in the oven, what's simmering, and what needs to come off the heat in the next five minutes. Meal Timer lets you queue every dish up front, start each one the moment it actually goes on the stove, and get a heads-up notification before it's done — so nothing overcooks while your attention is elsewhere.

## Features

- **Add dishes to a queue** with a name, cook duration, and a custom "alert me X minutes before done" offset
- **Fully concurrent timers** — cook as many dishes at once as you want; each one counts down independently
- **Background-safe** — timers keep running and alerts still fire even if the app isn't in the foreground, via a dedicated foreground service
- **Two-stage notifications** — a heads-up alert before the dish finishes, then a final "ready" notification
- **Live countdowns** in a clean, card-based dish list

## Tech stack & architecture

- **Language:** Java
- **Architecture:** MVVM (Activity → ViewModel → Repository → Room DAO)
- **Persistence:** Room, so the dish queue survives app restarts
- **Concurrency:** a single foreground `Service` drives all active timers off one shared tick loop, rather than one timer thread per dish
- **Notifications:** `NotificationManager` + notification channels, including the Android 13+ runtime permission flow

```
app/
├── data/         Room entity, DAO, database
├── repository/   Repository layer wrapping the DAO
├── service/      CookingTimerService — the concurrent timer engine
├── ui/           Activity, ViewModel, RecyclerView adapter, add-dish dialog
└── util/         Notification helper
```

## Why this project

Built as a portfolio piece to demonstrate real-world Android fundamentals beyond basic CRUD: background services that survive process death, scheduled notifications, concurrent state management, and a persistence layer — all wired together through a standard MVVM structure.

## Roadmap

- [ ] Pause/resume for an active timer
- [ ] Per-dish history log
- [ ] Default alert-offset preference
- [ ] Widget for at-a-glance active timers

## Screenshots

_Add a few screenshots or a short screen recording here once you have a build running._

## Getting started

1. Clone the repo
2. Open in Android Studio
3. Run on a device or emulator running API 26+ (API 33+ recommended, to exercise the notification permission flow)
