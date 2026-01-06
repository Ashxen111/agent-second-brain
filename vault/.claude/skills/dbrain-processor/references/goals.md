# Goals Integration

## ALWAYS Do First

Before processing daily entries:

1. **Read current focus:**

   Read goals/3-weekly.md → Extract ONE Big Thing

2. **Read yearly goals:**

   Read goals/1-yearly-2026.md → Know active goals by area

3. **Check monthly priorities:**

   Read goals/2-monthly-2026-01.md → Top 3 priorities

## Goal Alignment

When creating a task, ask:

1. **Does it connect to ONE Big Thing?**
   - Yes → add to task description: `→ Weekly focus`
   - No → continue checking

2. **Does it connect to monthly priority?**
   - Yes → add: `→ Monthly: [Priority name]`
   - No → continue checking

3. **Does it connect to yearly goal?**
   - Yes → add: `→ Goal: [Goal name]`
   - No → mark as "operational"

---

## Task Priority Boost

If task aligns with goals, consider priority bump:

| Alignment | Default | Boost to |

| ONE Big Thing | p3 | p1-p2 |
| Monthly priority | p3 | p2 |
| Yearly goal | p4 | p3 |
| No alignment | p4 | p4 |

---

## Saving Thoughts

When saving to thoughts/:

1. **Check goal relevance:**
   - Scan `goals/1-yearly-2026.md` for matching areas
   - If matches → add link in frontmatter:
yaml
     related:
       - "[[goals/1-yearly-2026#Career & Business]]"

2. **Tag with goal area:**

   #goal/career
   #goal/health  
   #goal/relationships
   #goal/growth
   #goal/financial

---

## Goal Progress Tracking

Track goal activity by:

- Task created → goal is "active"
- Thought saved → goal is "active"
- No activity 7+ days → "stale"
- No activity 14+ days → "warning"

---

## Report Section

Add to report:

```markdown
📈 Прогресс по целям:
{for each active yearly goal with recent activity:}
• {goal}: {progress}% {status_emoji}

{if stale goals:}
⚠️ Требует внимания:
• Цель "{goal}" без активности {days} дней
```

---

## Goal File Parsing

### 3-weekly.md — Find ONE Big Thing

Look for pattern:
markdown
> **If I accomplish nothing else, I will:**
> [THE ONE THING]

**Текущее (Week 01/2026):**
> Получить новый заказ на 60 тыс и предоплату

---

### 1-yearly-2026.md — Find Active Goals

Look for sections by life area:

```markdown
## Career & Business
### Goal 1: [Goal name]

## Health & Energy  
### Goal 1: [Goal name]

## Relationships
### Goal 1: [Goal name]

## Personal Growth
### Goal 1: [Goal name]

## Financial
### Goal 1: [Goal name]
```

**Текущие активные цели 2026:**

- **Career**: 5-6 крупных проектов (300-500 тыс), доход 300 тыс/мес
- **Health**: Вылечить зубы, ежедневная зарядка, бассейн 1 раз/неделю
- **Relationships**: Авторитет в комьюнити (2000 подписчиков, 2-3 кейса), 2-3 глубокие связи
- **Growth**: Самодисциплина, работа с установками
- **Financial**: 300 тыс/мес, закрыть долг 600 тыс

---

### 2-monthly.md — Find Top 3

Look for section:

```markdown
## Top 3 Priorities

### Priority 1: [Priority name]
### Priority 2: [Priority name]  
### Priority 3: [Priority name]
```

**Текущие приоритеты (Январь 2026):**

1. **Получить 2-3 средних проекта, 150 тыс** → связано с Financial + Career
2. **Развитие ТГ-канала и рост скиллов** → связано с Relationships + Growth
3. **Доделать бот-ассистент** → связано с Career (инфраструктура)

---

## Example Alignment

### Пример 1: Клиентская задача

**Entry:** "Созвон с Сергеем в 13:00, показать контент завод"

**Check:**

- ONE Big Thing: "Получить заказ на 60 тыс" → ❌ Не напрямую (но необходимо для дохода)
- Monthly #1: "Получить 2-3 средних проекта, 150 тыс" → ✅ Связано (Сергей платит 20 тыс)
- Yearly: "Financial: 300 тыс/мес" → ✅ Связано

**Result:**

Task: Созвон с Сергеем 13:00 - демо контент завода
Description: → Monthly: Получить 2-3 средних проекта
            → Goal: Financial 300 тыс/мес
Priority: p1 (клиентский дедлайн)

---

### Пример 2: Маркетинг

**Entry:** "Запостить рекламу на канал вайбкодинга"

**Check:**

- ONE Big Thing: "Получить заказ на 60 тыс" → ✅ Прямая связь (привлечение клиентов)
- Monthly #1: "Получить 2-3 средних проекта" → ✅ Связано
- Monthly #2: "Развитие ТГ-канала" → ✅ Связано
- Yearly: "Relationships: Авторитет в комьюнити" → ✅ Связано

**Result:**

Task: Разместить рекламу на канал вайбкодинга
Description: → Weekly focus (привлечение клиентов)
            → Monthly: Приоритеты #1 + #2
            → Goal: Авторитет в комьюнити
Priority: p2 (boosted from p3)

---

### Пример 3: Личное развитие

**Entry:** "Записать в дневник инсайт о самосаботаже"

**Check:**

- ONE Big Thing: "Получить заказ на 60 тыс" → ❌ Не связано напрямую
- Monthly priorities → ❌ Не в топ-3 января
- Yearly: "Growth: Работа с установками" → ✅ Связано

**Result:**

Thought: thoughts/reflections/2026-01-06-self-sabotage-pattern.md
Tags: #goal/growth #reflection #self-sabotage
Related: [[goals/1-yearly-2026#Personal Growth]]
Priority: p3 (стратегическое, не срочное)

---

### Пример 4: Обучение

**Entry:** "Изучил новую фичу n8n для работы с AI агентами"

**Check:**

- ONE Big Thing → ❌ Не связано
- Monthly #2: "Рост скиллов" → ✅ Связано
- Yearly: "Career: Стать экспертом" → ✅ Связано

**Result:**

Thought: thoughts/learnings/2026-01-06-n8n-ai-agents.md
Tags: #goal/career #learning #n8n
Related: [[goals/1-yearly-2026#Career & Business]]
Priority: p3

---

## Integration Rules

**Rule 1:** Любая задача, связанная с клиентами (Сергей, Лиза, Евгения) автоматически:

- → Monthly Priority #1
- → Yearly Goal: Financial
- Priority: p1-p2

**Rule 2:** Любой контент/маркетинг автоматически:

- → Monthly Priority #2
- → Yearly Goal: Relationships (авторитет)
- Priority: p2-p3

**Rule 3:** Работа над ботом-ассистентом:

- → Monthly Priority #3
- → Yearly Goal: Career (инфраструктура)
- Priority: p2

**Rule 4:** Личное развитие (рефлексия, каббала, психоанализ):

- → Yearly Goal: Growth
- Priority: p3-p4 (важно, но не срочно)

**Rule 5:** Здоровье (зубы, зарядка, бассейн):

- → Yearly Goal: Health
- Priority: p3 (если не срочное)

---

## Weekly Review Trigger

At end of week, generate:

```markdown
## Weekly Goal Review

### ONE Big Thing: {achieved/not achieved}
- Получить заказ на 60 тыс: {✅/❌}

### Monthly Progress:
1. Проекты (150 тыс): {X тыс заработано}
2. ТГ-канал: {текущее кол-во подписчиков}/{цель}
3. Бот-ассистент: {%готовности}

### Goal Activity:
- Active: {list of goals with tasks this week}
- Stale: {goals without activity 7+ days}
