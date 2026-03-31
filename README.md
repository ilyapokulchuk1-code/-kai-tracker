<!DOCTYPE html>

<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KAI Production — Трекер команды</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&display=swap');

:root {
–bg: #0c0c0e;
–surface: #141416;
–card: #1a1a1e;
–border: #2a2a30;
–gold: #d4a843;
–gold-dim: #8a6a26;
–gold-glow: rgba(212,168,67,0.12);
–white: #f0ede8;
–muted: #6b6870;
–done: #4caf7d;
–done-bg: rgba(76,175,125,0.08);
–red: #e05c5c;
}

- { box-sizing: border-box; margin: 0; padding: 0; }

body {
background: var(–bg);
color: var(–white);
font-family: ‘DM Sans’, sans-serif;
font-size: 14px;
min-height: 100vh;
line-height: 1.6;
}

/* HEADER */
.header {
padding: 40px 40px 0;
display: flex;
justify-content: space-between;
align-items: flex-end;
border-bottom: 1px solid var(–border);
padding-bottom: 28px;
}

.logo {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 48px;
letter-spacing: 4px;
color: var(–gold);
text-shadow: 0 0 40px rgba(212,168,67,0.3);
line-height: 1;
}

.logo-sub {
font-size: 11px;
letter-spacing: 3px;
color: var(–muted);
text-transform: uppercase;
margin-top: 4px;
}

.header-meta {
text-align: right;
}

.week-label {
font-size: 11px;
letter-spacing: 2px;
color: var(–muted);
text-transform: uppercase;
margin-bottom: 4px;
}

.week-date {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 22px;
color: var(–white);
letter-spacing: 2px;
}

/* NAV TABS */
.nav {
display: flex;
gap: 4px;
padding: 24px 40px 0;
border-bottom: 1px solid var(–border);
}

.nav-tab {
padding: 10px 22px 12px;
font-size: 12px;
letter-spacing: 2px;
text-transform: uppercase;
color: var(–muted);
cursor: pointer;
border-bottom: 2px solid transparent;
transition: all 0.2s;
font-weight: 500;
background: none;
border-top: none;
border-left: none;
border-right: none;
}

.nav-tab:hover { color: var(–white); }
.nav-tab.active {
color: var(–gold);
border-bottom-color: var(–gold);
}

/* LAYOUT */
.main {
padding: 32px 40px 60px;
}

.page { display: none; }
.page.active { display: block; }

/* PROGRESS BAR TOP */
.progress-banner {
background: var(–card);
border: 1px solid var(–border);
border-radius: 12px;
padding: 20px 24px;
margin-bottom: 28px;
display: flex;
align-items: center;
gap: 24px;
}

.progress-banner .progress-label {
font-size: 11px;
letter-spacing: 2px;
text-transform: uppercase;
color: var(–muted);
white-space: nowrap;
min-width: 80px;
}

.progress-bar-wrap {
flex: 1;
height: 6px;
background: var(–border);
border-radius: 3px;
overflow: hidden;
}

.progress-bar-fill {
height: 100%;
background: linear-gradient(90deg, var(–gold-dim), var(–gold));
border-radius: 3px;
transition: width 0.4s ease;
}

.progress-pct {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 22px;
color: var(–gold);
min-width: 50px;
text-align: right;
letter-spacing: 1px;
}

/* SECTION TITLE */
.section-title {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 28px;
letter-spacing: 3px;
color: var(–white);
margin-bottom: 4px;
}

.section-sub {
font-size: 12px;
color: var(–muted);
letter-spacing: 1px;
margin-bottom: 20px;
}

/* TASK CARD */
.task-group {
margin-bottom: 32px;
}

.task-group-title {
font-size: 10px;
letter-spacing: 3px;
text-transform: uppercase;
color: var(–gold);
margin-bottom: 10px;
display: flex;
align-items: center;
gap: 10px;
}

.task-group-title::after {
content: ‘’;
flex: 1;
height: 1px;
background: var(–border);
}

.task-item {
background: var(–card);
border: 1px solid var(–border);
border-radius: 10px;
padding: 14px 18px;
margin-bottom: 8px;
display: flex;
align-items: flex-start;
gap: 14px;
cursor: pointer;
transition: all 0.2s;
position: relative;
overflow: hidden;
}

.task-item::before {
content: ‘’;
position: absolute;
left: 0; top: 0; bottom: 0;
width: 3px;
background: var(–border);
transition: background 0.2s;
}

.task-item:hover {
border-color: var(–gold-dim);
background: #1e1e24;
}

.task-item:hover::before { background: var(–gold-dim); }

.task-item.done {
background: var(–done-bg);
border-color: rgba(76,175,125,0.25);
}

.task-item.done::before { background: var(–done); }

.task-checkbox {
width: 20px;
height: 20px;
border: 2px solid var(–border);
border-radius: 5px;
flex-shrink: 0;
margin-top: 1px;
display: flex;
align-items: center;
justify-content: center;
transition: all 0.2s;
background: var(–surface);
}

.task-item.done .task-checkbox {
background: var(–done);
border-color: var(–done);
}

.task-checkbox svg {
opacity: 0;
transition: opacity 0.15s;
}

.task-item.done .task-checkbox svg { opacity: 1; }

.task-content { flex: 1; }

.task-title {
font-size: 14px;
font-weight: 500;
color: var(–white);
transition: color 0.2s;
line-height: 1.4;
}

.task-item.done .task-title {
color: var(–muted);
text-decoration: line-through;
text-decoration-color: var(–muted);
}

.task-hint {
font-size: 12px;
color: var(–muted);
margin-top: 3px;
font-style: italic;
line-height: 1.4;
}

.task-tag {
font-size: 10px;
letter-spacing: 1.5px;
text-transform: uppercase;
padding: 3px 9px;
border-radius: 20px;
white-space: nowrap;
flex-shrink: 0;
align-self: flex-start;
margin-top: 2px;
}

.tag-setup { background: rgba(212,168,67,0.1); color: var(–gold); border: 1px solid var(–gold-dim); }
.tag-content { background: rgba(138,100,200,0.1); color: #a07fd0; border: 1px solid rgba(138,100,200,0.3); }
.tag-profile { background: rgba(80,160,220,0.1); color: #70b0e0; border: 1px solid rgba(80,160,220,0.3); }
.tag-strategy { background: rgba(220,100,80,0.1); color: #e07060; border: 1px solid rgba(220,100,80,0.3); }

/* WEEK PLANNER */
.week-grid {
display: grid;
grid-template-columns: repeat(7, 1fr);
gap: 8px;
margin-bottom: 28px;
}

.day-card {
background: var(–card);
border: 1px solid var(–border);
border-radius: 10px;
padding: 14px 10px;
min-height: 180px;
}

.day-name {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 16px;
letter-spacing: 2px;
color: var(–gold);
margin-bottom: 10px;
display: block;
}

.day-task {
font-size: 11px;
padding: 5px 8px;
border-radius: 6px;
margin-bottom: 5px;
line-height: 1.3;
cursor: pointer;
display: flex;
align-items: flex-start;
gap: 6px;
transition: opacity 0.2s;
}

.day-task.done { opacity: 0.45; }

.day-task.reel { background: rgba(138,100,200,0.12); color: #c0a0f0; border-left: 2px solid #a07fd0; }
.day-task.story { background: rgba(212,168,67,0.08); color: #d4b866; border-left: 2px solid var(–gold-dim); }
.day-task.edu { background: rgba(80,160,220,0.08); color: #80c0e8; border-left: 2px solid #5090c0; }

.day-task-check {
width: 12px;
height: 12px;
border: 1px solid currentColor;
border-radius: 3px;
flex-shrink: 0;
margin-top: 1px;
display: flex;
align-items: center;
justify-content: center;
font-size: 8px;
}

.day-task.done .day-task-check::after { content: ‘✓’; }

/* HIGHLIGHTS */
.highlights-grid {
display: grid;
grid-template-columns: repeat(3, 1fr);
gap: 12px;
margin-bottom: 32px;
}

.highlight-card {
background: var(–card);
border: 1px solid var(–border);
border-radius: 12px;
padding: 18px;
}

.highlight-num {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 13px;
letter-spacing: 2px;
color: var(–gold);
margin-bottom: 6px;
}

.highlight-name {
font-size: 13px;
font-weight: 500;
margin-bottom: 8px;
color: var(–white);
}

.highlight-tasks {
list-style: none;
}

.highlight-task {
font-size: 12px;
color: var(–muted);
padding: 5px 0;
border-bottom: 1px solid var(–border);
display: flex;
align-items: flex-start;
gap: 8px;
cursor: pointer;
transition: color 0.2s;
}

.highlight-task:last-child { border-bottom: none; }
.highlight-task:hover { color: var(–white); }
.highlight-task.done { color: var(–done); text-decoration: line-through; opacity: 0.6; }

.hl-check {
width: 14px;
height: 14px;
border: 1px solid var(–border);
border-radius: 3px;
flex-shrink: 0;
margin-top: 1px;
display: flex;
align-items: center;
justify-content: center;
font-size: 9px;
}

.highlight-task.done .hl-check {
background: var(–done);
border-color: var(–done);
color: white;
}

.highlight-task.done .hl-check::after { content: ‘✓’; }

/* KPI TABLE */
.kpi-grid {
display: grid;
grid-template-columns: repeat(2, 1fr);
gap: 10px;
margin-bottom: 32px;
}

.kpi-card {
background: var(–card);
border: 1px solid var(–border);
border-radius: 10px;
padding: 16px 18px;
display: flex;
justify-content: space-between;
align-items: center;
}

.kpi-label {
font-size: 13px;
color: var(–muted);
max-width: 200px;
line-height: 1.4;
}

.kpi-target {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 20px;
color: var(–gold);
letter-spacing: 1px;
white-space: nowrap;
}

/* TIPS */
.tip-box {
background: var(–gold-glow);
border: 1px solid var(–gold-dim);
border-radius: 10px;
padding: 16px 20px;
margin-bottom: 12px;
display: flex;
gap: 14px;
}

.tip-icon {
font-size: 18px;
flex-shrink: 0;
margin-top: 1px;
}

.tip-content {}

.tip-title {
font-size: 13px;
font-weight: 500;
color: var(–gold);
margin-bottom: 4px;
}

.tip-body {
font-size: 12px;
color: var(–muted);
line-height: 1.6;
}

/* CTA EXAMPLES */
.cta-list {
display: grid;
grid-template-columns: repeat(2, 1fr);
gap: 8px;
margin-bottom: 24px;
}

.cta-item {
background: var(–card);
border: 1px solid var(–border);
border-radius: 8px;
padding: 12px 16px;
font-size: 13px;
color: var(–white);
}

.cta-bad {
border-left: 3px solid var(–red);
opacity: 0.6;
}

.cta-good {
border-left: 3px solid var(–done);
}

.cta-label {
font-size: 10px;
text-transform: uppercase;
letter-spacing: 1.5px;
margin-bottom: 5px;
}

.cta-bad .cta-label { color: var(–red); }
.cta-good .cta-label { color: var(–done); }

/* PROFILES BIO */
.bio-variants {
display: grid;
grid-template-columns: repeat(2, 1fr);
gap: 12px;
margin-bottom: 28px;
}

.bio-card {
background: var(–card);
border: 1px solid var(–border);
border-radius: 10px;
padding: 16px;
cursor: pointer;
transition: all 0.2s;
}

.bio-card:hover { border-color: var(–gold-dim); }
.bio-card.selected { border-color: var(–gold); background: var(–gold-glow); }

.bio-num {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 12px;
letter-spacing: 2px;
color: var(–gold);
margin-bottom: 8px;
}

.bio-text {
font-size: 12.5px;
color: var(–white);
line-height: 1.7;
font-family: monospace;
}

/* FORMULA */
.formula-row {
display: flex;
align-items: center;
gap: 8px;
margin-bottom: 24px;
flex-wrap: wrap;
}

.formula-step {
background: var(–card);
border: 1px solid var(–border);
border-radius: 8px;
padding: 10px 18px;
font-size: 12px;
letter-spacing: 1px;
color: var(–white);
text-align: center;
}

.formula-arrow {
color: var(–gold);
font-size: 16px;
flex-shrink: 0;
}

/* STORY PLAN */
.story-week {
display: grid;
grid-template-columns: 1fr;
gap: 8px;
margin-bottom: 24px;
}

.story-row {
background: var(–card);
border: 1px solid var(–border);
border-radius: 8px;
padding: 12px 16px;
display: grid;
grid-template-columns: 100px 1fr;
gap: 16px;
align-items: start;
}

.story-day-name {
font-size: 11px;
letter-spacing: 2px;
text-transform: uppercase;
color: var(–gold);
font-weight: 500;
padding-top: 2px;
}

.story-day-theme {
font-size: 11px;
color: var(–muted);
letter-spacing: 1px;
font-style: italic;
}

.story-items {
display: flex;
flex-direction: column;
gap: 4px;
}

.story-s {
font-size: 12px;
color: var(–white);
line-height: 1.5;
padding: 4px 0;
border-bottom: 1px solid var(–border);
cursor: pointer;
display: flex;
gap: 8px;
}

.story-s:last-child { border-bottom: none; }
.story-s.done { color: var(–muted); text-decoration: line-through; opacity: 0.5; }

.story-check {
width: 14px;
height: 14px;
border: 1px solid var(–border);
border-radius: 3px;
flex-shrink: 0;
margin-top: 2px;
}

.story-s.done .story-check {
background: var(–done);
border-color: var(–done);
}

/* RESET BTN */
.reset-btn {
background: none;
border: 1px solid var(–border);
color: var(–muted);
padding: 8px 18px;
border-radius: 6px;
font-size: 11px;
letter-spacing: 1.5px;
text-transform: uppercase;
cursor: pointer;
transition: all 0.2s;
margin-bottom: 24px;
font-family: ‘DM Sans’, sans-serif;
}

.reset-btn:hover { color: var(–red); border-color: var(–red); }

/* SCROLLBAR */
::-webkit-scrollbar { width: 6px; }
::-webkit-scrollbar-track { background: var(–bg); }
::-webkit-scrollbar-thumb { background: var(–border); border-radius: 3px; }
</style>

</head>
<body>

<div class="header">
  <div>
    <div class="logo">KAI PRODUCTION</div>
    <div class="logo-sub">Трекер команды — Семестр 1</div>
  </div>
  <div class="header-meta">
    <div class="week-label">Текущий прогресс</div>
    <div class="week-date" id="today-date"></div>
  </div>
</div>

<nav class="nav">
  <button class="nav-tab active" onclick="showPage('setup')">🚀 Старт (шаги)</button>
  <button class="nav-tab" onclick="showPage('week')">📅 Неделя</button>
  <button class="nav-tab" onclick="showPage('stories')">📱 Сторис-план</button>
  <button class="nav-tab" onclick="showPage('highlights')">⭐ Highlights</button>
  <button class="nav-tab" onclick="showPage('tips')">💡 Советы</button>
  <button class="nav-tab" onclick="showPage('kpi')">📊 Метрики</button>
</nav>

<div class="main">

  <!-- ═══════════ SETUP PAGE ═══════════ -->

  <div class="page active" id="page-setup">

```
<div class="progress-banner">
  <span class="progress-label">Готово</span>
  <div class="progress-bar-wrap">
    <div class="progress-bar-fill" id="main-progress" style="width:0%"></div>
  </div>
  <span class="progress-pct" id="main-pct">0%</span>
</div>

<div class="section-title">ПЕРВЫЕ ШАГИ</div>
<div class="section-sub">Всё что нужно сделать прямо сейчас — расставлено по приоритету</div>

<!-- BIO -->
<div class="task-group">
  <div class="task-group-title">Профиль Instagram</div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">Сменить BIO в Instagram</div>
      <div class="task-hint">Выбрать один из 4 вариантов ниже во вкладке "Советы" → скопировать → вставить в профиль</div>
    </div>
    <span class="task-tag tag-profile">Профиль</span>
  </div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">Добавить форму сотрудничества в ссылку профиля</div>
      <div class="task-hint">Форма должна спрашивать: название бизнеса, индустрию, тип видео, бюджет, контакты (телефон + email)</div>
    </div>
    <span class="task-tag tag-setup">Срочно</span>
  </div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">Создать/обновить Highlights в нужном порядке</div>
      <div class="task-hint">Порядок: CLIENTS → CASES → BACKSTAGE → OFFERS/PACHETE → (опц. FAQ). Подробнее — вкладка "Highlights"</div>
    </div>
    <span class="task-tag tag-profile">Профиль</span>
  </div>
</div>

<!-- REELS -->
<div class="task-group">
  <div class="task-group-title">Контент — Reels (2 в неделю)</div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">Снять Reel #1 — Кинематографичный (о бренде / атмосфера / процесс)</div>
      <div class="task-hint">Brand film, детали бизнеса, атмосфера — показывает КТО вы, а не ЧТО продаёте</div>
    </div>
    <span class="task-tag tag-content">Рилс</span>
  </div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">Снять Reel #2 — Образовательный (советы об имидже бизнеса)</div>
      <div class="task-hint">Например: "Почему видео не продаёт", "3 ошибки в видео-контенте бренда", "Как выглядит доверие на экране"</div>
    </div>
    <span class="task-tag tag-content">Рилс</span>
  </div>
</div>

<!-- STORIES -->
<div class="task-group">
  <div class="task-group-title">Stories — каждый день или через день</div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">Снять сторис с началом недели + новый проект</div>
      <div class="task-hint">Структура: начало (контекст) → действие (что происходит) → вопрос или CTA</div>
    </div>
    <span class="task-tag tag-content">Сторис</span>
  </div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">Снять сторис Behind the scenes (Вторник)</div>
      <div class="task-hint">"Мы на съёмке. Показываем камеры и процесс. Вы когда-нибудь видели как создаётся brand film?"</div>
    </div>
    <span class="task-tag tag-content">Сторис</span>
  </div>
</div>

<!-- STRATEGY SETUP -->
<div class="task-group">
  <div class="task-group-title">Стратегические задачи</div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">Опубликовать первый Reel с CTA на форму</div>
      <div class="task-hint">Первый видео после смены BIO — должен вести в форму сотрудничества</div>
    </div>
    <span class="task-tag tag-strategy">Конверсия</span>
  </div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">Создать YouTube канал + 4 плейлиста</div>
      <div class="task-hint">Плейлисты: Brand Films / Educational / Behind The Scenes / Client Results. Загрузить первый Short.</div>
    </div>
    <span class="task-tag tag-setup">Месяц 3</span>
  </div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">Войти в 3 локальные бизнес-группы на Facebook</div>
      <div class="task-hint">Таргет: молдавские предприниматели 30–55 лет. Перераспределить видео туда.</div>
    </div>
    <span class="task-tag tag-setup">Месяц 2</span>
  </div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">Написать первый пост в Threads</div>
      <div class="task-hint">Тема: «Проблема не в контенте — в направлении» / короткое мнение, 3–6 строк</div>
    </div>
    <span class="task-tag tag-setup">Месяц 2-3</span>
  </div>
</div>

<button class="reset-btn" onclick="resetSetup()">↺ Сбросить галочки</button>
```

  </div>

  <!-- ═══════════ WEEK PAGE ═══════════ -->

  <div class="page" id="page-week">

```
<div class="section-title">ПЛАН НЕДЕЛИ</div>
<div class="section-sub">Нажимай на задачу — отмечай выполненное</div>

<div class="week-grid">
  <!-- MON -->
  <div class="day-card">
    <span class="day-name">ПОН</span>
    <div class="day-task reel" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>🎬 Снять Reel #1 (кинематограф)</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>📱 Сторис: начало недели + проект</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>📱 Сторис: что сегодня делаем</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>❓ Сторис: вопрос аудитории о видео</span>
    </div>
  </div>
  <!-- TUE -->
  <div class="day-card">
    <span class="day-name">ВТ</span>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>🎥 Сторис: мы на съёмке</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>📷 Сторис: показываем камеры</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>❓ Сторис: видели ли вы brand film?</span>
    </div>
  </div>
  <!-- WED -->
  <div class="day-card">
    <span class="day-name">СР</span>
    <div class="day-task edu" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>🎬 Снять Reel #2 (образовательный)</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>📚 Сторис: видео ≠ просто съёмка</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>💡 Сторис: premium = свет + storytelling</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>❓ Когда выбирали бизнес из-за вида?</span>
    </div>
  </div>
  <!-- THU -->
  <div class="day-card">
    <span class="day-name">ЧТ</span>
    <div class="day-task reel" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>📤 Опубликовать Reel #1</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>🏥 Сторис: работали с клиникой</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>🎬 Сторис: кадры из видео</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>❓ Видео меняет восприятие бренда?</span>
    </div>
  </div>
  <!-- FRI -->
  <div class="day-card">
    <span class="day-name">ПТ</span>
    <div class="day-task edu" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>📤 Опубликовать Reel #2</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>📖 Сторис: история предпринимателя</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>👤 Сторис: показываем команду/автора</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>❓ Какой бизнес в Кишинёве лучше всего представлен?</span>
    </div>
  </div>
  <!-- SAT -->
  <div class="day-card">
    <span class="day-name">СБ</span>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>✨ Сторис: вдохновение в деталях</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>🌟 Сторис: premium атмосфера</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>❓ Атмосфера места важна для вас?</span>
    </div>
  </div>
  <!-- SUN -->
  <div class="day-card">
    <span class="day-name">ВС</span>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>🔄 Сторис: итоги недели — проекты</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>🎬 Сторис: моменты со съёмок</span>
    </div>
    <div class="day-task story" onclick="toggleDay(this)">
      <div class="day-task-check"></div>
      <span>❓ Какой бизнес в Молдове заслуживает brand film?</span>
    </div>
  </div>
</div>

<button class="reset-btn" onclick="resetWeek()">↺ Новая неделя — сбросить</button>
```

  </div>

  <!-- ═══════════ STORIES PAGE ═══════════ -->

  <div class="page" id="page-stories">

```
<div class="section-title">ПЛАН СТОРИС</div>
<div class="section-sub">3 сторис в день по схеме: начало → действие → вопрос/CTA</div>

<div class="story-week">

  <div class="story-row">
    <div>
      <div class="story-day-name">Понедельник</div>
      <div class="story-day-theme">Начало недели</div>
    </div>
    <div class="story-items">
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 1: Начинаем неделю с нового видеопроекта.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 2: Сегодня работаем над концепцией brand film.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 3: Вы думаете, что видео влияет на решение клиента?</span></div>
    </div>
  </div>

  <div class="story-row">
    <div>
      <div class="story-day-name">Вторник</div>
      <div class="story-day-theme">Behind the scenes</div>
    </div>
    <div class="story-items">
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 1: Мы на съёмке.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 2: Показываем камеры и процесс.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 3: Вы когда-нибудь видели, как создаётся brand film?</span></div>
    </div>
  </div>

  <div class="story-row">
    <div>
      <div class="story-day-name">Среда</div>
      <div class="story-day-theme">Образование</div>
    </div>
    <div class="story-items">
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 1: Многие думают, что видео для бизнеса — это просто съёмка.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 2: Premium изображение = свет + storytelling.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 3: Когда вы последний раз выбирали бизнес, потому что он хорошо выглядит онлайн?</span></div>
    </div>
  </div>

  <div class="story-row">
    <div>
      <div class="story-day-name">Четверг</div>
      <div class="story-day-theme">Кейс клиента</div>
    </div>
    <div class="story-items">
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 1: Работали с клиникой. Показываем результат.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 2: Показываем кадры из видео.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 3: Вы верите, что видео меняет восприятие бренда?</span></div>
    </div>
  </div>

  <div class="story-row">
    <div>
      <div class="story-day-name">Пятница</div>
      <div class="story-day-theme">История предпринимателя</div>
    </div>
    <div class="story-items">
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 1: За каждым бизнесом — своя история.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 2: Показываем предпринимателя или команду.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 3: Какой бизнес в Кишинёве, по-вашему, лучше всего представлен?</span></div>
    </div>
  </div>

  <div class="story-row">
    <div>
      <div class="story-day-name">Суббота</div>
      <div class="story-day-theme">Lifestyle / Вдохновение</div>
    </div>
    <div class="story-items">
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 1: Вдохновение приходит из деталей.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 2: Показываем premium атмосферу.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 3: Для вас важна атмосфера места?</span></div>
    </div>
  </div>

  <div class="story-row">
    <div>
      <div class="story-day-name">Воскресенье</div>
      <div class="story-day-theme">Рефлексия</div>
    </div>
    <div class="story-items">
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 1: На этой неделе работали над интересными проектами.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 2: Показываем моменты со съёмок.</span></div>
      <div class="story-s" onclick="toggleStory(this)"><div class="story-check"></div><span>Story 3: Какой бизнес в Молдове заслуживает brand film?</span></div>
    </div>
  </div>
</div>

<button class="reset-btn" onclick="resetStories()">↺ Сбросить для новой недели</button>
```

  </div>

  <!-- ═══════════ HIGHLIGHTS PAGE ═══════════ -->

  <div class="page" id="page-highlights">

```
<div class="section-title">HIGHLIGHTS INSTAGRAM</div>
<div class="section-sub">Расставить именно в этом порядке — это первое что видит потенциальный клиент</div>

<div class="highlights-grid">

  <div class="highlight-card">
    <div class="highlight-num">01 — ПЕРВЫЙ</div>
    <div class="highlight-name">CLIENTS</div>
    <ul class="highlight-tasks">
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Видео-отзывы клиентов</span></li>
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Before/After результаты</span></li>
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Результаты в цифрах</span></li>
      <li class="highlight-task done" onclick="toggleHL(this)"><div class="hl-check"></div><span>Цель: социальное доказательство + доверие</span></li>
    </ul>
  </div>

  <div class="highlight-card">
    <div class="highlight-num">02</div>
    <div class="highlight-name">CASES</div>
    <ul class="highlight-tasks">
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Клиент + его проблема</span></li>
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Что вы сделали</span></li>
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Результат (бизнес-показатели)</span></li>
      <li class="highlight-task done" onclick="toggleHL(this)"><div class="hl-check"></div><span>Цель: связать видео с бизнес-результатами</span></li>
    </ul>
  </div>

  <div class="highlight-card">
    <div class="highlight-num">03</div>
    <div class="highlight-name">BACKSTAGE</div>
    <ul class="highlight-tasks">
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Making-of видео</span></li>
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Кадры со съёмок</span></li>
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Команда за работой</span></li>
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Световое оборудование, режиссура</span></li>
      <li class="highlight-task done" onclick="toggleHL(this)"><div class="hl-check"></div><span>Цель: показать — вы студия, не одиночный видеограф</span></li>
    </ul>
  </div>

  <div class="highlight-card">
    <div class="highlight-num">04</div>
    <div class="highlight-name">OFFERS / ПАКЕТЫ</div>
    <ul class="highlight-tasks">
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Слайд: KAI START</span></li>
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Слайд: KAI SIGNATURE</span></li>
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Слайд: KAI CAMPAIGN</span></li>
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Без цен — только состав пакета</span></li>
      <li class="highlight-task done" onclick="toggleHL(this)"><div class="hl-check"></div><span>Цель: ясность без обесценивания</span></li>
    </ul>
  </div>

  <div class="highlight-card">
    <div class="highlight-num">05 — опциональный</div>
    <div class="highlight-name">FAQ VIDEO</div>
    <ul class="highlight-tasks">
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Вопрос о цене — короткий ответ</span></li>
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Вопрос о времени производства</span></li>
      <li class="highlight-task" onclick="toggleHL(this)"><div class="hl-check"></div><span>Вопрос о камере/оборудовании</span></li>
      <li class="highlight-task done" onclick="toggleHL(this)"><div class="hl-check"></div><span>Цель: фильтровать и успокоить серьёзных клиентов</span></li>
    </ul>
  </div>

</div>

<div class="section-title" style="margin-top:20px">ФОРМУЛА ПОЗИЦИОНИРОВАНИЯ</div>
<div class="section-sub" style="margin-bottom:16px">Вы продаёте не видео. Вы продаёте:</div>
<div class="formula-row">
  <div class="formula-step">Восприятие</div>
  <span class="formula-arrow">+</span>
  <div class="formula-step">Позиционирование</div>
  <span class="formula-arrow">+</span>
  <div class="formula-step">Притяжение</div>
  <span class="formula-arrow">+</span>
  <div class="formula-step">Конверсию</div>
  <span class="formula-arrow">→</span>
  <div class="formula-step" style="color:var(--gold)">Видео = инструмент</div>
</div>
```

  </div>

  <!-- ═══════════ TIPS PAGE ═══════════ -->

  <div class="page" id="page-tips">

```
<div class="section-title">ВАРИАНТЫ BIO</div>
<div class="section-sub">Нажми на вариант который нравится — отметь его</div>

<div class="bio-variants">
  <div class="bio-card" onclick="selectBio(this)">
    <div class="bio-num">ВАРИАНТ 1</div>
    <div class="bio-text">Kai Production | Video Marketing 🎬<br>Превращаем визуал в продажи<br>+6 лет | бренды, которые растут онлайн<br>Reels & storytelling которые конвертируют<br>👉 Применить для сотрудничества</div>
  </div>
  <div class="bio-card" onclick="selectBio(this)">
    <div class="bio-num">ВАРИАНТ 2</div>
    <div class="bio-text">Kai Production 🎬<br>Видеопроизводство для брендов, которые хотят продавать<br>+6 лет опыта | стратегия + исполнение<br>Кинематографичный контент, который привлекает клиентов<br>👉 Применить сейчас</div>
  </div>
  <div class="bio-card" onclick="selectBio(this)">
    <div class="bio-num">ВАРИАНТ 3</div>
    <div class="bio-text">Kai Production 🎬<br>Мы не просто снимаем. Строим контент, который продаёт.<br>+6 лет в видео & маркетинге<br>Для брендов, которым нужны реальные результаты<br>👉 Работать с нами</div>
  </div>
  <div class="bio-card" onclick="selectBio(this)">
    <div class="bio-num">ВАРИАНТ 4</div>
    <div class="bio-text">Kai Production 🎬<br>Контент, который заставляет остановиться & хотеть больше<br>+6 лет в видео & маркетинге<br>Бренды растут через storytelling<br>👉 Войти в процесс</div>
  </div>
</div>

<div class="section-title" style="margin-top:8px">CTA — ЧТО ГОВОРИТЬ</div>
<div class="section-sub">Правильные призывы к действию — не «напиши мне»</div>

<div class="cta-list">
  <div class="cta-item cta-bad">
    <div class="cta-label">❌ Не использовать</div>
    «Напишите мне»
  </div>
  <div class="cta-item cta-good">
    <div class="cta-label">✓ Использовать</div>
    «Открой для себя»
  </div>
  <div class="cta-item cta-bad">
    <div class="cta-label">❌ Не использовать</div>
    «Применить»
  </div>
  <div class="cta-item cta-good">
    <div class="cta-label">✓ Использовать</div>
    «Следи за процессом»
  </div>
  <div class="cta-item cta-good">
    <div class="cta-label">✓ Использовать</div>
    «Наблюдай разницу»
  </div>
  <div class="cta-item cta-good">
    <div class="cta-label">✓ Использовать</div>
    «Посмотри, как выглядит правильно построенный бренд»
  </div>
</div>

<div class="section-title">СОВЕТЫ ДЛЯ ТВОРЧЕСКИХ ЛЮДЕЙ</div>
<div class="section-sub" style="margin-bottom:16px">Как не потерять структуру и сохранить энергию</div>

<div class="tip-box">
  <div class="tip-icon">🎯</div>
  <div class="tip-content">
    <div class="tip-title">Один фокус на неделю</div>
    <div class="tip-body">Не думайте о всём одновременно. В начале недели выберите одну тему недели (кейс клиента / процесс / обучение) — и всё снимаете вокруг неё. Меньше решений = больше энергии на съёмку.</div>
  </div>
</div>

<div class="tip-box">
  <div class="tip-icon">📦</div>
  <div class="tip-content">
    <div class="tip-title">Батч-съёмка</div>
    <div class="tip-body">Выберите один день в неделю (например вторник) — снимайте сразу 5–7 сторис и оба рилса. Потом просто публикуйте по расписанию. Творческим людям это даёт свободу быть в потоке, а не снимать каждый день.</div>
  </div>
</div>

<div class="tip-box">
  <div class="tip-icon">⚡</div>
  <div class="tip-content">
    <div class="tip-title">Структура сторис — 3 шага</div>
    <div class="tip-body"><strong style="color:var(--gold)">Начало</strong> — контекст (где вы, что происходит)<br><strong style="color:var(--gold)">Действие</strong> — что именно показываете<br><strong style="color:var(--gold)">Вопрос/CTA</strong> — вовлекаем или направляем в форму</div>
  </div>
</div>

<div class="tip-box">
  <div class="tip-icon">🔍</div>
  <div class="tip-content">
    <div class="tip-title">Метрики — что смотреть в реелсах</div>
    <div class="tip-body">Видеопросмотры 3000–5000+ → значит тема зашла<br>Сохранения (Save) → признак образовательной ценности<br>Репосты (Share) → высокий интерес<br>Конверсии в форму → главная цель всего</div>
  </div>
</div>

<div class="tip-box">
  <div class="tip-icon">🚫</div>
  <div class="tip-content">
    <div class="tip-title">Каких клиентов НЕ брать</div>
    <div class="tip-body">«Сколько стоит видео?» без контекста — не ваш клиент<br>«Быстро, дёшево, на завтра» — нет<br>Хотят вирального видео без бизнес-цели — нет<br>Бюджет ниже 300–500€ (KAI START) — нет</div>
  </div>
</div>
```

  </div>

  <!-- ═══════════ KPI PAGE ═══════════ -->

  <div class="page" id="page-kpi">

```
<div class="section-title">МЕТРИКИ И KPI</div>
<div class="section-sub">Цели после 3-го месяца. Заполняй еженедельно.</div>

<div class="kpi-grid">
  <div class="kpi-card">
    <div class="kpi-label">Входящие запросы (формы + DM) в месяц</div>
    <div class="kpi-target">20+ / мес</div>
  </div>
  <div class="kpi-card">
    <div class="kpi-label">Запланированных и проведённых звонков</div>
    <div class="kpi-target">10–15 / мес</div>
  </div>
  <div class="kpi-card">
    <div class="kpi-label">Конверсия звонок → коммерческое предложение</div>
    <div class="kpi-target">70%</div>
  </div>
  <div class="kpi-card">
    <div class="kpi-label">Конверсия КП → клиент</div>
    <div class="kpi-target">40–50%</div>
  </div>
  <div class="kpi-card">
    <div class="kpi-label">Новых подписанных клиентов в месяц</div>
    <div class="kpi-target">4 минимум</div>
  </div>
  <div class="kpi-card">
    <div class="kpi-label">Средний чек (Signature)</div>
    <div class="kpi-target">1.900€</div>
  </div>
  <div class="kpi-card">
    <div class="kpi-label">Сохранений на один Reel</div>
    <div class="kpi-target">30+ / рилс</div>
  </div>
  <div class="kpi-card">
    <div class="kpi-label">DM из видео</div>
    <div class="kpi-target">3–5 / рилс</div>
  </div>
  <div class="kpi-card">
    <div class="kpi-label">Накопленных кейсов за 6 месяцев</div>
    <div class="kpi-target">10 кейсов</div>
  </div>
</div>

<div class="section-title" style="margin-top:8px">ВОПРОСЫ КОНЦА МЕСЯЦА</div>
<div class="section-sub">Отвечайте честно — минимум 6 месяцев подряд. Это ваш компас.</div>

<div class="task-group">
  <div class="task-group-title">Ежемесячный анализ — 4 вопроса</div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">1. Какой ТИП клиента принёс больше всего денег и лучшие проекты?</div>
      <div class="task-hint">Запишите ответ — это ваш идеальный клиент на следующий месяц</div>
    </div>
  </div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">2. Какой ТИП контента принёс больше всего качественных лидов?</div>
      <div class="task-hint">Кинематографичный или образовательный? Кейс или behind the scenes?</div>
    </div>
  </div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">3. Какое ВОЗРАЖЕНИЕ встречалось чаще всего — и как ответить в контенте?</div>
      <div class="task-hint">Превратить возражение в тему рилса или сторис следующего месяца</div>
    </div>
  </div>

  <div class="task-item" onclick="toggleTask(this)">
    <div class="task-checkbox"><svg width="11" height="9" viewBox="0 0 11 9"><polyline points="1,4 4,8 10,1" stroke="white" stroke-width="2" fill="none" stroke-linecap="round"/></svg></div>
    <div class="task-content">
      <div class="task-title">4. Какие ПРОЕКТЫ отказали — и правильно ли это было для позиционирования?</div>
      <div class="task-hint">Отказ от плохого проекта = защита бренда Kai Production</div>
    </div>
  </div>
</div>
```

  </div>

</div>

<script>
  // Date
  const d = new Date();
  const days = ['Воскресенье','Понедельник','Вторник','Среда','Четверг','Пятница','Суббота'];
  const months = ['января','февраля','марта','апреля','мая','июня','июля','августа','сентября','октября','ноября','декабря'];
  document.getElementById('today-date').textContent = `${days[d.getDay()]}, ${d.getDate()} ${months[d.getMonth()]}`;

  function showPage(id) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
    document.getElementById('page-' + id).classList.add('active');
    event.target.classList.add('active');
  }

  function toggleTask(el) {
    el.classList.toggle('done');
    updateProgress();
  }

  function toggleDay(el) {
    el.classList.toggle('done');
  }

  function toggleStory(el) {
    el.classList.toggle('done');
  }

  function toggleHL(el) {
    el.classList.toggle('done');
    const check = el.querySelector('.hl-check');
    if (el.classList.contains('done')) {
      check.textContent = '✓';
    } else {
      check.textContent = '';
    }
  }

  function selectBio(el) {
    document.querySelectorAll('.bio-card').forEach(c => c.classList.remove('selected'));
    el.classList.add('selected');
  }

  function updateProgress() {
    const items = document.querySelectorAll('#page-setup .task-item');
    const done = document.querySelectorAll('#page-setup .task-item.done');
    const pct = items.length ? Math.round((done.length / items.length) * 100) : 0;
    document.getElementById('main-progress').style.width = pct + '%';
    document.getElementById('main-pct').textContent = pct + '%';
  }

  function resetSetup() {
    document.querySelectorAll('#page-setup .task-item').forEach(el => el.classList.remove('done'));
    updateProgress();
  }

  function resetWeek() {
    document.querySelectorAll('#page-week .day-task').forEach(el => el.classList.remove('done'));
  }

  function resetStories() {
    document.querySelectorAll('#page-stories .story-s').forEach(el => el.classList.remove('done'));
  }

  updateProgress();
</script>

</body>
</html>
