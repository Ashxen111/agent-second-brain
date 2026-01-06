# Todoist Integration

## Available MCP Tools

### Reading Tasks

- `get-overview` — all projects with hierarchy
- `find-tasks` — search by text, project, section
- `find-tasks-by-date` — tasks by date range

### Writing Tasks

- `add-tasks` — create new tasks
- `complete-tasks` — mark as done
- `update-tasks` — modify existing

---

## Pre-Creation Checklist

### 1. Check Workload (REQUIRED)

find-tasks-by-date:
  startDate: "today"
  daysCount: 7
  limit: 50

Build workload map:

Mon: 2 tasks
Tue: 4 tasks  ← overloaded
Wed: 1 task
Thu: 3 tasks  ← at limit
Fri: 2 tasks
Sat: 0 tasks
Sun: 0 tasks

### 2. Check Duplicates (REQUIRED)

find-tasks:
  searchText: "key words from new task"

If similar exists → mark as duplicate, don't create.

---

## Priority by Domain

Based on user's work context (see [ABOUT.md](ABOUT.md)):

| Domain | Default Priority | Override |

| Client Work | p1-p2 | — |
| Agency Ops (urgent) | p2 | — |
| Agency Ops (regular) | p3 | — |
| Content (with deadline) | p2-p3 | — |
| Product/R&D | p4 | масштабируемость → p3 |
| AI & Tech | p4 | автоматизация → p3 |
| Personal | p3-p4 | — |

### Priority Keywords

| Keywords in text | Priority |

| срочно, критично, дедлайн клиента | p1 |
| важно, приоритет, до конца недели | p2 |
| нужно, надо, не забыть | p3 |
| (strategic, R&D, long-term) | p4 |

### Apply Decision Filters for Priority Boost

If entry matches 2+ filters → boost priority by 1 level:

- Это масштабируется?
- Это можно автоматизировать?
- Это усиливает экспертизу/бренд?
- Это приближает к продукту/SaaS?

---

## Date Mapping

| Context | dueString |

| **Client deadline** | exact date |
| **Urgent ops** | today / tomorrow |
| **This week** | friday |
| **Next week** | next monday |
| **Strategic/R&D** | in 7 days |
| **Not specified** | in 3 days |

### Russian → dueString

| Russian | dueString |

| сегодня | today |
| завтра | tomorrow |
| послезавтра | in 2 days |
| в понедельник | monday |
| во вторник | tuesday |
| в среду | wednesday |
| в четверг | thursday |
| в пятницу | friday |
| в субботу | saturday |
| в воскресенье | sunday |
| на этой неделе | friday |
| на следующей неделе | next monday |
| через неделю | in 7 days |
| к концу месяца | January 31 |
| 15 января | January 15 |

---

## Task Creation

add-tasks:
  tasks:
    - content: "Task title"
      dueString: "friday"  # MANDATORY
      priority: "p4"       # based on domain
      projectId: "..."     # if known

### Task Title Style

User prefers: прямота, ясность, конкретика

<!-- Замените примеры на релевантные для вас -->
✅ Good:

- "Созвон с Сергеем 13:00 - демо контент завода"
- "Разместить рекламу на канал вайбкодинга"
- "Доделать систему оповещений бот-ассистента"
- "Написать пост про автоматизацию для ТГ"
- "Донастроить парсинг лидов"

❌ Bad:

- "Подумать о презентации"
- "Что-то с клиентом"
- "Разобраться с AI"
- "Поработать над проектом"

### Workload Balancing

If target day has 3+ tasks:

1. Find next day with < 3 tasks
2. Use that day instead
3. Mention in report: "сдвинуто на {day} (перегрузка)"

---

## Project Detection

<!--
Настройте под свои проекты в Todoist.
Замените примеры клиентов и название канала.
-->

| Keywords | Project |

| Сергей, Лиза, Евгения, клиент, проект, заказ, оплата | Клиентские проекты |
| автоматизация бизнеса, финансы, долг, планирование, самозанятый | Управление бизнесом |
| бот-ассистент, продукт, подписка, монетизация, фича | Продукт (Бот) |
| пост, Ашхен Гудкова, AI & Магия автоматизации, ТГ, кейс, контент | Контент & Маркетинг |
| реклама, лиды, каналы, вайбкодинг, парсинг, подписчики | Маркетинг & Лиды |
| n8n, обучение, курс, технология, скилл | Обучение & Развитие |
| психоанализ, каббала, рефлексия, зубы, зарядка, здоровье | Личное |

If unclear → use Inbox (no projectId).

---

## Specific Task Patterns

### Клиентские задачи

Pattern: `{клиент} + {действие}`

Examples:

- Сергей: доделать контент завод → p1, today/tomorrow
- Лиза: созвон по проекту → p1, конкретная дата
- Евгения: отправить отчёт → p2, friday

### Маркетинговые задачи

Pattern: `разместить/запостить на {канал}`

Examples:

- Разместить рекламу на канал вайбкодинга → p2, today
- Пост в ТГ про автоматизацию → p3, wednesday
- Донастроить парсинг лидов → p3, friday

### Задачи по боту

Pattern: `бот-ассистент: {фича/действие}`

Examples:

- Бот-ассистент: система оповещений → p2, friday
- Бот-ассистент: настроить оплату → p2, monday
- Бот-ассистент: тестирование → p2, sunday

### Контент

Pattern: `пост/кейс про {тема}`

Examples:

- Пост в ТГ про n8n кейс → p3, wednesday
- Записать голосовое про автоматизацию → p3, saturday
- Опубликовать кейс "контент завод" → p3, next week

---

## Anti-Patterns (НЕ СОЗДАВАТЬ)

Based on user preferences:

- ❌ "Подумать о..." → конкретизируй действие
- ❌ "Разобраться с..." → что именно сделать?
- ❌ "Поработать над..." → какой конкретный результат?
- ❌ Абстрактные задачи без Next Action
- ❌ Дубликаты существующих задач
- ❌ Задачи без дат
- ❌ Задачи, не проходящие Decision Filters (деньги/обучение)

---

## Weekly ONE Big Thing Integration

Current week's ONE Big Thing affects priority:

**Week 01/2026:** "Получить новый заказ на 60 тыс и предоплату"

Tasks directly supporting ONE Big Thing get priority boost:

- Размещение рекламы → p2 (was p3)
- Парсинг лидов → p2 (was p3)  
- Работа с входящими заявками → p1 (was p2)

---

## Monthly Priority Integration

Current month: January 2026

Priority 1: "Получить 2-3 средних проекта, 150 тыс"
→ Все задачи по клиентам и лидогенерации: p1-p2

Priority 2: "Развитие ТГ-канала и рост скиллов"
→ Все задачи по контенту и обучению: p2-p3

Priority 3: "Доделать бот-ассистент"
→ Все задачи по боту: p2

---

## Example Task Creation

### Input Entry

"Созвон с Сергеем в 13:00, показать текущее состояние контент завода"

### Processing

1. Domain: Client Work (keyword: "Сергей")
2. Priority: p1 (клиент + дедлайн сегодня)
3. Date: "today" (срочно, конкретное время)
4. Project: "Клиентские проекты"
5. Workload check: Вт 6 янв уже 2 задачи → ОК (< 3)
6. Duplicate check: нет похожих
7. Decision Filters: ✅ деньги (оплата 20 тыс), ✅ новое (опыт)
8. Goal alignment: → Monthly #1, → Yearly: Financial

### Output

```yaml
add-tasks:
  tasks:
    - content: "Созвон с Сергеем 13:00 - демо контент завода"
      dueString: "today"
      priority: "p1"
      projectId: "[ID клиентских проектов]"
      description: "→ Monthly: Получить 2-3 проекта, 150 тыс
→ Goal: Financial 300 тыс/мес"
```

---

## Error Handling

CRITICAL: Никогда не предлагай "добавить вручную".

If `add-tasks` fails:

1. Include EXACT error message in report
2. Continue with next entry
3. Don't mark as processed
4. User will see error and can debug

WRONG output:

"Не удалось добавить (MCP недоступен). Добавь вручную: Task title"

CORRECT output:

"Ошибка создания задачи: [exact error from MCP tool]"

---

## Special Cases

### Recurring Tasks

If entry suggests recurring action:

"Каждый день размещать рекламу на один канал"

Create first instance only:

- content: "Разместить рекламу на канал #1"
  dueString: "today"
  priority: "p2"

Note in report: "Создана первая задача серии. Остальные создавай по мере выполнения."

### Batch Actions

If entry contains multiple similar tasks:

"Разместить рекламу на 6 каналов"

Create as separate tasks with different dates:

- Разместить рекламу на канал #1 → today
- Разместить рекламу на канал #2 → tomorrow  
- Разместить рекламу на канал #3 → thursday
...

Respect workload limits (max 3 per day).
