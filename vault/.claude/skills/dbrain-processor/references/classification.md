# Entry Classification

## Work Domains → Categories

Based on user's work context (see [ABOUT.md](ABOUT.md)):

### Client Work

Брифы, стратегии, автоматизации, проекты, оплаты, дедлайны

**Keywords:** Сергей, Лиза, Евгения, клиент, проект, бриф, дедлайн, оплата, предоплата, заказ, контент завод

**→ Category:** task (p1-p2) → Todoist

---

### AI & Tech

Инструменты, модели, автоматизации, боты, интеграции, n8n

**Keywords:** n8n, GPT, Claude, AI, модель, бот, автоматизация, интеграция, API, парсинг, бот-ассистент, оповещения

**→ Category:** learning или project → thoughts/

---

### Product

Идеи продуктов, бот-ассистент, SaaS, монетизация

**Keywords:** бот-ассистент, продукт, SaaS, подписка, монетизация, MVP, фича, функционал

**→ Category:** idea или project → thoughts/

---

### Company Ops

Финансы, планирование, процессы, автоматизация бизнеса

**Keywords:** финансы, доход, долг, оплата, бизнес-процесс, самозанятый, налоги, расходы, планирование

**→ Category:** task или project (depends on urgency)

---

### Content

Посты, идеи для Telegram-канала, кейсы, статьи

**Keywords:** пост, Ашхен Гудкова, AI & Магия автоматизации, ТГ-канал, контент, кейс, статья, голосовое, кружочки, подкаст

**→ Category:** idea → thoughts/ideas/ или task если с дедлайном

---

### Маркетинг и лидогенерация

Реклама, привлечение клиентов, рост подписчиков, каналы

**Keywords:** реклама, лиды, лидогенерация, подписчики, каналы, вайбкодинг, парсинг лидов, авторитет, комьюнити, отзывы

**→ Category:** task (p2-p3) или project → thoughts/

---

### Обучение и развитие

Новые технологии, скиллы, курсы, обучающие материалы

**Keywords:** курс, обучение, изучить, скилл, технология, научиться, освоить, прокачать, развитие

**→ Category:** learning → thoughts/learnings/

---

### Личное

Психоанализ, каббала, рефлексия, здоровье, отношения

**Keywords:** психоанализ, каббала, рефлексия, дневник, здоровье, зубы, зарядка, бассейн, отношения, партнёр, самодисциплина, установки

**→ Category:** reflection → thoughts/reflections/

---

## Decision Tree

Entry text contains...
│
├─ Клиент или дедлайн? ──────────────────────────> TASK (p1-p2)
│  (Сергей, Лиза, Евгения, клиент, дедлайн, оплата)
│
├─ Оперативное/срочное? ─────────────────────────> TASK (p2-p3)
│  (нужно сделать, не забыть, позвонить, встреча)
│
├─ Маркетинг/лиды? ──────────────────────────────> TASK (p2-p3) или PROJECT
│  (реклама, лиды, каналы, подписчики)
│
├─ AI/tech обучение? ────────────────────────────> LEARNING
│  (узнал, n8n, модель, бот, интеграция)
│
├─ Идея продукта/фичи? ──────────────────────────> IDEA или PROJECT
│  (бот-ассистент, продукт, SaaS, подписка)
│
├─ Стратегическое мышление? ─────────────────────> PROJECT
│  (стратегия, план, долгосрочно, агентство)
│
├─ Личный инсайт? ───────────────────────────────> REFLECTION
│  (понял, осознал, рефлексия, психоанализ)
│
└─ Идея контента? ───────────────────────────────> IDEA
   (пост, кейс, тезис, контент)

## Apply Decision Filters

Перед сохранением спроси:

- **Приносит ли это деньги?** (основной фильтр)
- **Научусь ли я чему-то новому?** (рост экспертизы)
- **Приближает ли к агентству на 30 человек?** (стратегия)
- **Есть ли ресурсы (время, энергия)?** (реалистичность)

Если да на 2+ вопроса → повысить приоритет.

---

## Photo Entries

For `[photo]` entries:

1. Analyze image content via vision
2. Determine domain:
   - Screenshot клиентского материала → Client Work
   - Схема/диаграмма автоматизации → AI & Tech
   - Скриншот статьи/обучения → Learning
   - Личное (зубы, здоровье) → Личное
3. Add description to daily file

---

## Output Locations

| Category | Destination | Priority |

| task (client) | Todoist | p1-p2 |
| task (marketing) | Todoist | p2-p3 |
| task (ops) | Todoist | p2-p3 |
| task (content) | Todoist | p3-p4 |
| idea | thoughts/ideas/ | — |
| reflection | thoughts/reflections/ | — |
| project | thoughts/projects/ | — |
| learning | thoughts/learnings/ | — |

---

## File Naming

thoughts/{category}/{YYYY-MM-DD}-short-title.md

Examples:

thoughts/ideas/2026-01-06-telegram-content-series.md
thoughts/projects/2026-01-06-bot-assistant-monetization.md
thoughts/learnings/2026-01-06-n8n-advanced-flows.md
thoughts/reflections/2026-01-06-self-sabotage-patterns.md

## Thought Structure

Use preferred format:

```markdown
---
date: {YYYY-MM-DD}
type: {category}
domain: {Client Work|AI & Tech|Product|Company Ops|Content|Marketing|Learning|Personal}
tags: [tag1, tag2]
---

## Контекст
[Что привело к мысли]

## Инсайт
[Ключевая идея]

## Что это значит
[Применение к моему бизнесу/агентству/целям]

## Следующее действие
[Конкретный шаг — не абстрактный]
```

---

## Anti-Patterns (ИЗБЕГАТЬ)

При создании мыслей НЕ делать:

- Абстрактные рассуждения без Следующего действия
- Теория без применения к автоматизации/клиентам
- Повторы без синтеза (кластеризуй похожие!)
- Хаотичные списки без приоритетов
- Задачи типа "подумать о..." (конкретизируй!)
- Идеи, которые не проходят Decision Filters (деньги + обучение)

---

## MOC Updates

After creating thought file, add link to:

MOC/MOC-{category}s.md

Group by domain when relevant:

```markdown
## AI & Tech
- [[2026-01-06-n8n-advanced-flows]] - Продвинутые автоматизации

## Product
- [[2026-01-06-bot-assistant-monetization]] - Монетизация бота

## Personal
- [[2026-01-06-self-sabotage-patterns]] - Работа с установками
```
