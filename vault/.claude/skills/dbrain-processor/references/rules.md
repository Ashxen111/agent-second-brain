# Critical Processing Rules

See [ABOUT.md](ABOUT.md) for user context and preferences.

---

## Rule 1: Skip Processed Entries

If entry contains `<!-- ✓ processed` → SKIP COMPLETELY

Check AFTER each `## HH:MM` header for the marker.

**Example:**

```markdown
## 13:00

Созвон с Сергеем - показать контент завод
<!-- ✓ processed: task → Todoist: Созвон с Сергеем p1 сегодня -->

→ **SKIP this entry completely**

---

## Rule 2: Every Task = Date

**NEVER create a task without `dueString`:**

| Text | dueString |

| завтра | tomorrow |
| в пятницу | friday |
| на этой неделе | friday |
| в четверг | thursday |
| 15 января | January 15 |
| к концу недели | sunday |
| на следующей неделе | next monday |
| сегодня | today |
| NOT SPECIFIED | in 3 days |

**Примеры из контекста Ашхен:**

| Фраза в записи | dueString | Обоснование |

| "Доделать к пятнице" | friday | Явный срок |
| "Созвон с Сергеем сегодня" | today | Срочно |
| "Запостить рекламу" | tomorrow | Регулярная задача |
| "Доделать бота к понедельнику" | next monday | Явный срок |

---

## Rule 3: Check Duplicates

**BEFORE creating any task:**

1. Call `find-tasks` with key words from task
2. If similar task exists → **DO NOT CREATE**
3. Mark as: `<!-- ✓ processed: task (duplicate) -->`

**Example:**

Entry: "Не забыть созвониться с Сергеем"
→ find-tasks: "Сергей созвон"
→ Found: "Созвон с Сергеем 13:00 - демо контент завода"
→ DO NOT CREATE
→ Mark: <!-- ✓ processed: task (duplicate) -->


**Common duplicates to watch for:**
- Клиенты: Сергей, Лиза, Евгения (проверять по имени)
- Бот-ассистент (много задач по нему)
- Реклама/посты в ТГ (ежедневные)
- Контент завод (проект Сергея)

---

## Rule 4: Consider Workload

**BEFORE creating tasks:**

1. Call `find-tasks-by-date` with `startDate: "today"`, `daysCount: 7`
2. Count tasks per day
3. If target day has 3+ tasks → shift to next day with less load

**Special consideration for Ашхен:**
- Она сова → предпочитает вечернюю работу
- Рабочая неделя: 6-8 часов фокуса в день
- Пятница-суббота: пик для крупных задач
- Воскресенье: более легкие задачи

**Example:**

Task: "Доработать бота"
Target: Friday
find-tasks-by-date → Friday has: Сергей тест, реклама, парсинг (3 задачи)
→ SHIFT to Saturday (2 задачи)


---

## Rule 5: Mark After Processing

After EACH processed entry, add marker:

```markdown
<!-- ✓ processed: {category} -->
```

**Categories:**

- `task` — создана задача в Todoist
- `thought` — сохранена мысль в thoughts/
- `skip` — запись не требует действий
- `duplicate` — дубликат существующей задачи
- `reflection` — личная рефлексия
- `context` — контекстная информация

**For tasks with details:**

```markdown
<!-- ✓ processed: task → Todoist: {name} {priority} {date} -->
```

**Examples:**

```markdown
<!-- ✓ processed: task → Todoist: Созвон с Сергеем p1 today -->
<!-- ✓ processed: thought → thoughts/ideas/2026-01-06-telegram-series.md -->
<!-- ✓ processed: skip (already in weekly plan) -->
<!-- ✓ processed: duplicate (exists: "Реклама на вайбкодинг") -->
```

---

## Rule 6: Apply Decision Filters

Before saving any thought or task, check Ашхен's filters:

1. **Приносит ли это деньги?** (основной фильтр)
2. **Научусь ли я чему-то новому?** (рост экспертизы)
3. **Приближает ли к агентству на 30 человек?** (стратегия)
4. **Есть ли ресурсы (время, энергия)?** (реалистичность)

If 2+ yes → boost priority.

## Rule 7: Avoid Anti-Patterns

**NEVER create:**

❌ **Абстрактные задачи без Next Action**

Bad: "Подумать о монетизации бота"
Good: "Определить 3 модели монетизации бота - изучить конкурентов"

❌ **Хаотичные списки без приоритетов**

Bad: "Сделать: пост, реклама, бот, обучение, звонки..."
Good: Разбить на отдельные задачи с приоритетами и датами

❌ **Повторы без синтеза**

Bad: Создавать 5 задач "Запостить рекламу на канал X"
Good: Одна задача "Рекламная кампания: 6 каналов" с чеклистом

❌ **Академическая теория без применения**

Bad: "Изучить теорию маркетинга"
Good: "Применить модель AIDA к рекламному посту для вайбкодинга"

❌ **Задачи, не проходящие Decision Filters**

Bad: "Переделать дизайн сайта" (нет денег, нет обучения, не критично)
Good: "Добавить кейс Сергея на сайт" (привлечение клиентов → деньги)

See [ABOUT.md](ABOUT.md) → Anti-Patterns section for full list.

---

## Special Rules for Ашхен's Context

### Client Work (Сергей, Лиза, Евгения)

- **Always p1-p2** (деньги + срочность)
- **Always connect to:** `→ Monthly: Priority #1` + `→ Goal: Financial`
- **Check deadline carefully** — клиентские дедлайны священны

### Marketing & Content

- **Daily posts/ads** → batch into weekly task with checklist
- **Always connect to:** `→ Monthly: Priority #2` + `→ Goal: Relationships`
- **Track metrics:** подписчики, просмотры, лиды

### Bot Assistant

- **Current focus** → `→ Monthly: Priority #3`
- **System improvements** → thoughts/projects/
- **Bugs** → p1, **Features** → p2-p3

### Personal (Психоанализ, Каббала, Здоровье)

- **Default p3-p4** (важно, но не срочно)
- **Always connect to:** `→ Goal: Growth` or `→ Goal: Health`
- **Exception:** срочное медицинское → p2

---

## Checklist Before Completion

Before finishing processing, verify:

- [ ] All new entries processed (no entries without `<!-- ✓ processed`)
- [ ] No duplicates in Todoist (used `find-tasks` before creating)
- [ ] All tasks have dates via `dueString` (no tasks without dates)
- [ ] All tasks have concrete actions (no "подумать о...")
- [ ] Decision filters applied (2+ yes or explicitly noted why not)
- [ ] Anti-patterns avoided (no abstract tasks, no chaos)
- [ ] Client work is p1-p2 (Сергей, Лиза, Евгения)
- [ ] Weekly ONE Big Thing considered (связь с получением заказа 60 тыс)
- [ ] Workload balanced (не более 3-4 задач на день)
- [ ] MOC files updated (if created thoughts)
- [ ] Report generated with goal progress

---

## Report Template

```markdown
## 📊 Обработка записей за [date]

### Создано:
- ✅ Задачи: {count} ({p1}/{p2}/{p3}/{p4})
- 💭 Мысли: {count} (ideas/projects/learnings/reflections)
- ⏭️ Пропущено: {count} (дубликаты, уже обработано)

### Связь с целями:
- 🎯 ONE Big Thing (заказ 60 тыс): {X задач}
- 📅 Monthly Priority #1 (проекты 150к): {X задач}
- 📅 Monthly Priority #2 (ТГ-канал): {X задач}
- 📅 Monthly Priority #3 (бот): {X задач}

### Приоритеты:
- 🔴 p1 (срочно): {list}
- 🟠 p2 (важно): {list}
- 🟡 p3 (стратегия): {list}
- ⚪ p4 (когда-нибудь): {list}

### ⚠️ Требует внимания:
- {issues or warnings if any}

### 📈 Прогресс по целям:
{см. goals-integration.md для формата}
```

---

## Emergency Override

If entry explicitly says "срочно", "дедлайн", "горит", "критично":
→ IGNORE workload balancing
→ Set p1
→ Use specified date or today
