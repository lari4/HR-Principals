# Agent Workflows Documentation

## Содержание

1. [Пайплайн оценки кандидатов](#1-пайплайн-оценки-кандидатов)
2. [Пайплайн карьерного консультирования](#2-пайплайн-карьерного-консультирования)
3. [Интерактивные пайплайны](#3-интерактивные-пайплайны)
4. [Технические детали](#4-технические-детали)

---

## 1. Пайплайн оценки кандидатов

### Описание
Основной пайплайн для оценки кандидатов на позицию Discord Architect. Использует два AI агента (Philosopher и Prophet) для комплексного анализа профиля кандидата с разных перспектив.

### Файл
`src/main.py` → `HRTeam.evaluate_application()`

### Участники
- **Talent Philosopher (Agent_P)** - философская оценка
- **Candidate Prophet (Agent_C)** - пророческая оценка

### ASCII схема потока данных

```
┌─────────────────────────────────────────────────────────────────────┐
│                    ПАЙПЛАЙН ОЦЕНКИ КАНДИДАТОВ                       │
└─────────────────────────────────────────────────────────────────────┘

    ┌──────────────────┐
    │  Входные данные  │
    │  (CSV файл)      │
    │  - name          │
    │  - role          │
    │  - application   │
    │  - background    │
    └────────┬─────────┘
             │
             ▼
    ┌────────────────────────────┐
    │ ApplicationProcessor       │
    │ load_applications()        │
    └────────┬───────────────────┘
             │
             ▼
    ┌─────────────────────────────────────┐
    │  UI: Welcome Animation + Progress   │
    │  - Initializing AI Agents           │
    │  - Loading Candidate Profile        │
    │  - Analyzing Background             │
    │  - Processing Experience            │
    │  - Evaluating Cultural Fit          │
    │  - Generating Insights              │
    └────────┬────────────────────────────┘
             │
             ▼
    ┌─────────────────────────────────────────────────────────┐
    │              ЭТАП 1: ФИЛОСОФСКАЯ ОЦЕНКА                 │
    └─────────────────────────────────────────────────────────┘
             │
             ▼
    ┌────────────────────────────┐
    │  Talent Philosopher        │
    │  evaluate_candidate()      │
    │                            │
    │  Промпт:                   │
    │  *examining the            │
    │   candidate's journey      │
    │   with philosophical       │
    │   curiosity*               │
    │                            │
    │  Analyze this candidate's  │
    │  background with           │
    │  philosophical depth:      │
    │  {resume_data}             │
    │                            │
    │  Consider:                 │
    │  1. Hidden patterns        │
    │  2. Unconventional         │
    │     strengths              │
    │  3. Philosophical          │
    │     implications           │
    │  4. Future trajectories    │
    └────────┬───────────────────┘
             │
             │  phil_analysis
             │  ────────────────►
             ▼
    ┌────────────────────────────┐
    │  conversation_history      │
    │  .append(("philosopher",   │
    │           phil_analysis))  │
    └────────┬───────────────────┘
             │
             ▼
    ┌─────────────────────────────────────────────────────────┐
    │              ЭТАП 2: ПРОРОЧЕСКАЯ ОЦЕНКА                 │
    └─────────────────────────────────────────────────────────┘
             │
             ▼
    ┌────────────────────────────┐
    │  Candidate Prophet         │
    │  evaluate_candidate()      │
    │                            │
    │  Промпт:                   │
    │  *receiving visions of     │
    │   the candidate's          │
    │   potential futures*       │
    │                            │
    │  Divine the hidden         │
    │  potential in this         │
    │  profile:                  │
    │  {resume_data}             │
    │                            │
    │  Focus on:                 │
    │  1. Future impact          │
    │     trajectories           │
    │  2. Latent talents         │
    │  3. Unexpected synergies   │
    │  4. Growth catalysts       │
    └────────┬───────────────────┘
             │
             │  prophet_vision
             │  ────────────────►
             ▼
    ┌────────────────────────────┐
    │  conversation_history      │
    │  .append(("prophet",       │
    │           prophet_vision)) │
    └────────┬───────────────────┘
             │
             ▼
    ┌─────────────────────────────────────────────────────────┐
    │           ЭТАП 3: ГЕНЕРАЦИЯ ОТЧЕТА                      │
    └─────────────────────────────────────────────────────────┘
             │
             ▼
    ┌────────────────────────────┐
    │  generate_evaluation_      │
    │  report()                  │
    │                            │
    │  Данные из:                │
    │  - phil_analysis           │
    │  - prophet_vision          │
    │  - application_data        │
    │                            │
    │  Вычисляет:                │
    │  ├─ community_vision       │
    │  │  ├─ moderation         │
    │  │  ├─ education          │
    │  │  ├─ engagement         │
    │  │  └─ overall            │
    │  ├─ technical_capability   │
    │  │  ├─ discord_expertise  │
    │  │  ├─ automation         │
    │  │  ├─ integration        │
    │  │  └─ overall            │
    │  └─ cultural_alignment    │
    │     ├─ ai_passion         │
    │     ├─ community_mindset  │
    │     ├─ innovation         │
    │     └─ overall            │
    │                            │
    │  Генерирует:               │
    │  - Executive Summary       │
    │  - Detailed Assessment     │
    │  - Key Observations        │
    │  - Growth Potential        │
    │  - Risk Assessment         │
    │  - Unique Potential        │
    │  - Next Steps              │
    └────────┬───────────────────┘
             │
             │  report_data
             │  ────────────────►
             ▼
    ┌────────────────────────────┐
    │  Markdown отчет            │
    │  (выводится в консоль)     │
    └────────┬───────────────────┘
             │
             ▼
    ┌─────────────────────────────────────────────────────────┐
    │           ЭТАП 4: ИНТЕРАКТИВНАЯ СЕССИЯ                  │
    └─────────────────────────────────────────────────────────┘
             │
             ▼
    ┌────────────────────────────┐
    │  InteractiveSession        │
    │  start_interactive_        │
    │  session()                 │
    │                            │
    │  12 опций:                 │
    │  1. Chat with Principals   │
    │  2. Approve Candidate      │
    │  3. Reject Candidate       │
    │  4. Alternative Roles      │
    │  5. Deep Dive Analysis     │
    │  6. Custom Assessment      │
    │  7. Team Interaction       │
    │  8. Growth Roadmap         │
    │  9. Future Impact          │
    │  10. Competitive Analysis  │
    │  11. Suggest Improvements  │
    │  12. Exit                  │
    └────────┬───────────────────┘
             │
             ▼
    ┌────────────────────────────┐
    │  Цикл интерактивных        │
    │  сессий до выхода          │
    │  пользователя              │
    └────────────────────────────┘
```

### Передача данных между этапами

#### 1. Входные данные → Philosopher
```python
application_data = {
    'name': str,
    'role': str,
    'application': str,  # Полный текст заявки
    'background': str    # Бэкграунд кандидата
}
```

#### 2. Philosopher → conversation_history
```python
phil_analysis = {
    'type': 'text',
    'content': str,  # Философский анализ кандидата
    'insights': [...]  # Ключевые инсайты
}

conversation_history.append(("philosopher", phil_analysis))
```

#### 3. Входные данные → Prophet
```python
# Те же application_data
```

#### 4. Prophet → conversation_history
```python
prophet_vision = {
    'type': 'text',
    'content': str,  # Пророческое видение
    'predictions': [...]  # Предсказания
}

conversation_history.append(("prophet", prophet_vision))
```

#### 5. conversation_history → report_data
```python
report_data = {
    'scores': {
        'community_vision': {
            'moderation': float,
            'education': float,
            'engagement': float,
            'overall': float
        },
        'technical_capability': {
            'discord_expertise': float,
            'automation': float,
            'integration': float,
            'overall': float
        },
        'cultural_alignment': {
            'ai_passion': float,
            'community_mindset': float,
            'innovation': float,
            'overall': float
        }
    },
    'total_score': float,
    'recommendation': str,
    'strengths': {
        'community': [str],
        'technical': [str],
        'cultural': [str]
    },
    'development_areas': {
        'community': [str],
        'technical': [str],
        'cultural': [str]
    }
}
```

### Ключевые промпты

1. **Философская оценка** (`philosopher.evaluate_candidate()`)
   - Входные данные: `resume_data` (application_data)
   - Промпт: См. PROMPTS_DOCUMENTATION.md → 2.1
   - Выходные данные: Философский анализ кандидата

2. **Пророческая оценка** (`prophet.evaluate_candidate()`)
   - Входные данные: `resume_data` (application_data)
   - Промпт: См. PROMPTS_DOCUMENTATION.md → 2.3
   - Выходные данные: Пророческое видение потенциала

### Временная последовательность

1. **T0**: Загрузка данных из CSV
2. **T1**: Отображение UI анимации (~2-3 сек)
3. **T2**: Вызов Philosopher (~5-10 сек)
4. **T3**: Сохранение результата Philosopher
5. **T4**: Вызов Prophet (~5-10 сек)
6. **T5**: Сохранение результата Prophet
7. **T6**: Генерация отчета (~1 сек)
8. **T7**: Отображение отчета в консоли
9. **T8**: Запуск интерактивной сессии (бесконечный цикл до выхода)

### Примечания

- Оба агента работают **последовательно**, не параллельно
- Каждый агент получает **одинаковые входные данные**
- Агенты **не видят** результаты друг друга на этапе первичной оценки
- История сохраняется в `conversation_history` для последующих интерактивных сессий
- Оценки (scores) в отчете генерируются **после** получения обоих анализов

---

## 2. Пайплайн карьерного консультирования

### Описание
Пайплайн для карьерного консультирования и развития с использованием двух AI агентов (User Advocate и Strategist), которые ведут диалог между собой для выработки неконвенциональных карьерных рекомендаций.

### Файлы
- `src/agents/advocate.py` → `UserAdvocateAgent`
- `src/agents/strategist.py` → `StrategistAgent`

### Участники
- **User Advocate (Agent_U)** - защитник интересов пользователя, провокационный карьерный революционер
- **Career Strategist (Agent_S)** - визионер карьерного будущего, контрарианский мыслитель

### ASCII схема потока данных

```
┌─────────────────────────────────────────────────────────────────────┐
│               ПАЙПЛАЙН КАРЬЕРНОГО КОНСУЛЬТИРОВАНИЯ                  │
└─────────────────────────────────────────────────────────────────────┘

    ┌──────────────────┐
    │  Входные данные  │
    │  user_input:     │
    │  "Хочу сменить   │
    │   карьеру на AI" │
    └────────┬─────────┘
             │
             ▼
    ┌─────────────────────────────────────────────────────────┐
    │           ЭТАП 1: ВВЕДЕНИЕ КЕЙСА (ADVOCATE)             │
    └─────────────────────────────────────────────────────────┘
             │
             ▼
    ┌────────────────────────────┐
    │  User Advocate             │
    │  introduce_case()          │
    │                            │
    │  Промпт:                   │
    │  Based on this input:      │
    │  '{user_input}'            │
    │                            │
    │  Start a natural           │
    │  conversation with the     │
    │  Strategist about this     │
    │  case. Show your thinking  │
    │  and ask for initial       │
    │  thoughts.                 │
    └────────┬───────────────────┘
             │
             │  advocate_intro
             │  ────────────────────►
             │  *thinking about unconventional paths*
             │  "Hey Strategist, we've got someone
             │   wanting to switch to AI. But why
             │   traditional ML when quantum-neural
             │   interfaces are emerging? Thoughts?"
             ▼
    ┌─────────────────────────────────────────────────────────┐
    │           ЭТАП 2: АНАЛИЗ КЕЙСА (STRATEGIST)             │
    └─────────────────────────────────────────────────────────┘
             │
             ▼
    ┌────────────────────────────┐
    │  Career Strategist         │
    │  analyze_case()            │
    │                            │
    │  Промпт:                   │
    │  The User Advocate         │
    │  mentioned:                │
    │  {advocate_intro}          │
    │                            │
    │  Share your initial        │
    │  reaction and thoughts.    │
    │  Keep it brief and         │
    │  conversational, ask       │
    │  questions, show your      │
    │  thinking process.         │
    └────────┬───────────────────┘
             │
             │  strategist_analysis
             │  ────────────────────►
             │  *analyzing intersection of quantum
             │   computing and social media*
             │  "Interesting! But have you considered
             │   the neuro-symbolic programming angle?
             │   That's where real opportunity lies."
             ▼
    ┌─────────────────────────────────────────────────────────┐
    │        ЭТАП 3: ЗАПРОС РЕКОМЕНДАЦИЙ (ADVOCATE)           │
    └─────────────────────────────────────────────────────────┘
             │
             ▼
    ┌────────────────────────────┐
    │  User Advocate             │
    │  request_recommendations() │
    │                            │
    │  Промпт:                   │
    │  The Strategist has        │
    │  provided this analysis:   │
    │  {strategist_analysis}     │
    │                            │
    │  Request specific          │
    │  recommendations from      │
    │  the Strategist, focusing  │
    │  on:                       │
    │  - Practical next steps    │
    │  - Specific skills needed  │
    │  - Potential challenges    │
    │    to address              │
    │                            │
    │  Frame your request as     │
    │  part of the ongoing       │
    │  discussion.               │
    └────────┬───────────────────┘
             │
             │  advocate_request
             │  ────────────────────►
             │  "Love the neuro-symbolic angle!
             │   What specific skills should they
             │   focus on? Any non-obvious learning
             │   paths?"
             ▼
    ┌─────────────────────────────────────────────────────────┐
    │      ЭТАП 4: ПРЕДОСТАВЛЕНИЕ РЕКОМЕНДАЦИЙ (STRATEGIST)   │
    └─────────────────────────────────────────────────────────┘
             │
             ▼
    ┌────────────────────────────┐
    │  Career Strategist         │
    │  provide_recommendations() │
    │                            │
    │  Промпт:                   │
    │  The User Advocate has     │
    │  requested:                │
    │  {advocate_request}        │
    │                            │
    │  Provide detailed          │
    │  recommendations,          │
    │  addressing:               │
    │  - Specific skills to      │
    │    develop                 │
    │  - Learning resources      │
    │  - Career milestones       │
    │    to target               │
    │  - Industry connections    │
    │    to build                │
    │                            │
    │  Frame your response as    │
    │  part of the ongoing       │
    │  discussion with your      │
    │  fellow agents.            │
    └────────┬───────────────────┘
             │
             │  recommendations
             │  ────────────────────►
             │  "Focus on:
             │   1. Symbolic reasoning systems
             │   2. Quantum ML frameworks
             │   3. Join neuro-AI research groups
             │   Timeline: 6-12 months to pivot"
             ▼
    ┌─────────────────────────────────────────────────────────┐
    │      ЭТАП 5: СУММИРОВАНИЕ ДЛЯ ПОЛЬЗОВАТЕЛЯ (ADVOCATE)   │
    └─────────────────────────────────────────────────────────┘
             │
             ▼
    ┌────────────────────────────┐
    │  User Advocate             │
    │  summarize_                │
    │  recommendations()         │
    │                            │
    │  Промпт:                   │
    │  The Strategist has        │
    │  recommended:              │
    │  {recommendations}         │
    │                            │
    │  Summarize these           │
    │  recommendations for       │
    │  the user, making them:    │
    │  - Actionable and clear    │
    │  - Prioritized by          │
    │    importance              │
    │  - Tailored to their       │
    │    specific situation      │
    │                            │
    │  Frame this as a           │
    │  collaborative conclusion  │
    │  to our discussion.        │
    └────────┬───────────────────┘
             │
             │  user_summary
             │  ────────────────────►
             ▼
    ┌────────────────────────────┐
    │  Итоговые рекомендации     │
    │  для пользователя          │
    │                            │
    │  Приоритезированные,       │
    │  действенные советы        │
    └────────┬───────────────────┘
             │
             ▼
    ┌─────────────────────────────────────────────────────────┐
    │           ОПЦИОНАЛЬНО: ГЕНЕРАЦИЯ ОТЧЕТА                 │
    └─────────────────────────────────────────────────────────┘
             │
             ├──────────────────────────────────────────┐
             │                                          │
             ▼                                          ▼
    ┌────────────────────┐                  ┌────────────────────┐
    │  User Advocate     │                  │  Strategist        │
    │  generate_report_  │                  │  generate_report_  │
    │  section()         │                  │  section()         │
    │                    │                  │                    │
    │  Создает:          │                  │  Создает:          │
    │  - Learning path   │                  │  - Micro-niches    │
    │  - Project ideas   │                  │  - Skill combos    │
    │  - Networking ops  │                  │  - Tech convergence│
    │  - Contrarian moves│                  │  - Market timeline │
    │  - Resources       │                  │  - First-mover     │
    │                    │                  │    advantages      │
    └────────┬───────────┘                  └────────┬───────────┘
             │                                       │
             └───────────────┬───────────────────────┘
                             │
                             ▼
                  ┌────────────────────┐
                  │  Полный отчет в    │
                  │  формате Markdown  │
                  └────────────────────┘
```

### Передача данных между этапами

#### 1. user_input → Advocate
```python
user_input = str  # "Хочу сменить карьеру на AI"
```

#### 2. Advocate → Strategist (introduce_case)
```python
advocate_intro = {
    'type': 'text',
    'content': str,  # Провокационное введение кейса
    'questions': [str],  # Вопросы к Strategist
    'initial_thoughts': str  # Начальные мысли Advocate
}
```

#### 3. Strategist → Advocate (analyze_case)
```python
strategist_analysis = {
    'type': 'text',
    'content': str,  # Первичный анализ
    'insights': [str],  # Ключевые инсайты
    'counter_questions': [str]  # Вопросы обратно к Advocate
}
```

#### 4. Advocate → Strategist (request_recommendations)
```python
advocate_request = {
    'type': 'text',
    'content': str,  # Запрос конкретных рекомендаций
    'focus_areas': [
        'Practical next steps',
        'Specific skills needed',
        'Potential challenges to address'
    ]
}
```

#### 5. Strategist → Advocate (provide_recommendations)
```python
recommendations = {
    'type': 'text',
    'content': str,  # Детальные рекомендации
    'skills': [str],  # Навыки для развития
    'resources': [str],  # Ресурсы для обучения
    'milestones': [str],  # Карьерные вехи
    'connections': [str]  # Связи в индустрии
}
```

#### 6. Advocate → User (summarize_recommendations)
```python
user_summary = {
    'type': 'text',
    'content': str,  # Итоговое резюме
    'actionable_items': [
        {
            'action': str,
            'priority': int,  # 1-5
            'timeline': str,
            'rationale': str
        }
    ],
    'tailored_advice': str
}
```

### Ключевые промпты

1. **Введение кейса** (`advocate.introduce_case()`)
   - Входные данные: `user_input`
   - Промпт: Введение кейса для обсуждения
   - Выходные данные: Провокационное введение для Strategist

2. **Анализ кейса** (`strategist.analyze_case()`)
   - Входные данные: `advocate_intro`
   - Промпт: См. PROMPTS_DOCUMENTATION.md → 4.2.1
   - Выходные данные: Первичный анализ с контрарианской перспективой

3. **Запрос рекомендаций** (`advocate.request_recommendations()`)
   - Входные данные: `strategist_analysis`
   - Промпт: См. PROMPTS_DOCUMENTATION.md → 4.1.1
   - Выходные данные: Запрос конкретных действий

4. **Предоставление рекомендаций** (`strategist.provide_recommendations()`)
   - Входные данные: `advocate_request`
   - Промпт: См. PROMPTS_DOCUMENTATION.md → 4.2.1
   - Выходные данные: Детальные рекомендации

5. **Суммирование для пользователя** (`advocate.summarize_recommendations()`)
   - Входные данные: `recommendations`
   - Промпт: См. PROMPTS_DOCUMENTATION.md → 4.1.2
   - Выходные данные: Ясные, приоритезированные рекомендации

### Паттерн взаимодействия

```
Advocate: *thinking* + провокационный вопрос
   ↓
Strategist: *analyzing* + контрарианский ответ
   ↓
Advocate: Запрос конкретики
   ↓
Strategist: Детальные рекомендации
   ↓
Advocate: Резюме для пользователя
```

### Характеристики диалога

- **Стиль**: Сократический диалог с провокациями
- **Частота обмена**: 3-5 раундов на один кейс
- **Внутренний монолог**: Оба агента используют *звездочки* для мыслей
- **Фокус**: Неконвенциональные пути и будущие возможности

### Временная последовательность

1. **T0**: Получение запроса пользователя
2. **T1**: Advocate вводит кейс (~3-5 сек)
3. **T2**: Strategist анализирует (~3-5 сек)
4. **T3**: Advocate запрашивает рекомендации (~3-5 сек)
5. **T4**: Strategist предоставляет рекомендации (~5-10 сек)
6. **T5**: Advocate суммирует для пользователя (~3-5 сек)
7. **T6** (опционально): Генерация детальных отчетов (~5-10 сек каждый)

### Примечания

- Агенты работают в **диалоговом режиме**, последовательно
- Каждый агент **видит** предыдущие сообщения партнера
- Стиль общения - **провокационный и контрарианский**
- Фокус на **возникающих технологиях** и **гибридных ролях**
- Рекомендации всегда **неконвенциональные** и **перспективные**

---

## 3. Интерактивные пайплайны

### Описание
Набор из 12 интерактивных пайплайнов, которые активируются после первичной оценки кандидата. Пользователь выбирает одну из опций и система запускает соответствующий AI workflow.

### Файл
`src/main.py` → `InteractiveSession`

### Общая структура

```
┌─────────────────────────────────────────────────────────────────────┐
│                 ИНТЕРАКТИВНАЯ СЕССИЯ (ГЛАВНОЕ МЕНЮ)                 │
└─────────────────────────────────────────────────────────────────────┘

                    ┌──────────────────────┐
                    │ Выбор пользователя   │
                    │ (1-12)               │
                    └──────────┬───────────┘
                               │
            ┌──────────────────┼──────────────────┐
            │                  │                  │
            ▼                  ▼                  ▼
    ┌───────────────┐  ┌───────────────┐  ┌───────────────┐
    │ Категория 1:  │  │ Категория 2:  │  │ Категория 3:  │
    │ Диалоговые    │  │ Аналитические │  │ Процедурные   │
    │               │  │               │  │               │
    │ 1. Chat       │  │ 4. Alt Roles  │  │ 2. Approve    │
    │11. Improve    │  │ 5. Deep Dive  │  │ 3. Reject     │
    │               │  │ 6. Assessment │  │12. Exit       │
    │               │  │ 7. Team Sim   │  │               │
    │               │  │ 8. Roadmap    │  │               │
    │               │  │ 9. Impact     │  │               │
    │               │  │10. Competitive│  │               │
    └───────────────┘  └───────────────┘  └───────────────┘
```

---

### 3.1 Чат с Principals

**Назначение**: Интерактивный Q&A с AI агентами о кандидате

**ASCII схема**:
```
┌────────────────────────────────────────────────────────┐
│           ПАЙПЛАЙН: ЧАТ С PRINCIPALS                   │
└────────────────────────────────────────────────────────┘

    Вход: question (от пользователя)
      │
      ▼
    ┌──────────────────────────┐
    │ Формирование промпта:    │
    │ - Имя кандидата          │
    │ - Детали оценки          │
    │ - Бэкграунд кандидата    │
    │ - Требования PN          │
    │ - Вопрос пользователя    │
    └────────┬─────────────────┘
             │
             ├──────────────────┐
             │                  │
             ▼                  ▼
    ┌────────────────┐  ┌────────────────┐
    │  Philosopher   │  │    Prophet     │
    │  process_      │  │    process_    │
    │  message()     │  │    message()   │
    └────────┬───────┘  └────────┬───────┘
             │                   │
             ▼                   ▼
    ┌────────────────┐  ┌────────────────┐
    │ Phil Response  │  │ Prophet Response│
    └────────┬───────┘  └────────┬───────┘
             │                   │
             └─────────┬─────────┘
                       │
                       ▼
              ┌────────────────┐
              │ chat_history   │
              │ .append()      │
              └────────┬───────┘
                       │
                       ▼
              ┌────────────────┐
              │ Ответы выведены│
              │ пользователю   │
              └────────────────┘
                       │
                  (цикл до 'exit')
```

**Промпт**: См. PROMPTS_DOCUMENTATION.md → 4.4.1

**Передача данных**:
```python
input: question (str)
output: [phil_response (str), prophet_response (str)]
stored_in: chat_history[]
```

---

### 3.2 Approve/Reject кандидата

**ASCII схема**:
```
┌────────────────────────────────────────────────────────┐
│        ПАЙПЛАЙН: APPROVE/REJECT CANDIDATE              │
└────────────────────────────────────────────────────────┘

    Approve (option 2)              Reject (option 3)
         │                                │
         ▼                                ▼
    ┌──────────────┐              ┌──────────────┐
    │ Get approval │              │ Get rejection│
    │ notes        │              │ reason       │
    │ (optional)   │              │ (required)   │
    └──────┬───────┘              └──────┬───────┘
           │                              │
           ▼                              ▼
    ┌──────────────┐              ┌──────────────┐
    │ Confirm      │              │ Confirm      │
    │ (Yes/No)     │              │ (Yes/No)     │
    └──────┬───────┘              └──────┬───────┘
           │                              │
           ▼                              ▼
    ┌──────────────┐              ┌──────────────┐
    │ Display      │              │ Display      │
    │ confirmation │              │ confirmation │
    │ panel:       │              │ panel:       │
    │ - Name       │              │ - Name       │
    │ - Role       │              │ - Role       │
    │ - Notes      │              │ - Reason     │
    │ - Timestamp  │              │ - Timestamp  │
    └──────────────┘              └──────────────┘
```

**Передача данных**:
```python
Approve:
  input: notes (str, optional)
  output: confirmation_panel

Reject:
  input: reason (str, required)
  output: confirmation_panel
```

---

### 3.3 Alternative Roles

**Назначение**: Предложение альтернативных позиций для кандидата

**ASCII схема**:
```
┌────────────────────────────────────────────────────────┐
│          ПАЙПЛАЙН: АЛЬТЕРНАТИВНЫЕ РОЛИ                 │
└────────────────────────────────────────────────────────┘

    Входные данные:
    - application (candidate profile)
      │
      ▼
    ┌──────────────────────────┐
    │ Формирование промпта:    │
    │ - Профиль кандидата      │
    │ - Результаты оценки      │
    │ - Уникальные навыки      │
    │ - Потенциал              │
    └────────┬─────────────────┘
             │
             ▼
    ┌────────────────────────┐
    │  Philosopher           │
    │  process_message()     │
    │                        │
    │  "Suggest alternative  │
    │   roles at Principals  │
    │   Network where they   │
    │   might excel..."      │
    └────────┬───────────────┘
             │
             ▼
    ┌────────────────────────┐
    │ Альтернативные роли:   │
    │ - Role 1 + rationale   │
    │ - Role 2 + rationale   │
    │ - Role 3 + rationale   │
    └────────────────────────┘
```

**Промпт**: См. PROMPTS_DOCUMENTATION.md → 4.4.2

**Передача данных**:
```python
input: application (dict)
output: alternative_roles_suggestions (str)
```

---

### 3.4 Deep Dive Analysis

**Назначение**: Углубленный анализ конкретного аспекта кандидата

**ASCII схема**:
```
┌────────────────────────────────────────────────────────┐
│           ПАЙПЛАЙН: DEEP DIVE ANALYSIS                 │
└────────────────────────────────────────────────────────┘

    Пользователь выбирает аспект:
    ┌──────────────────────┐
    │ - Technical Depth    │
    │ - Community Lead     │
    │ - Innovation         │
    │ - Cultural Impact    │
    │ - Growth Trajectory  │
    └────────┬─────────────┘
             │
             ▼
    ┌──────────────────────┐
    │ Формирование промпта:│
    │ "Perform deep dive   │
    │  analysis of the     │
    │  candidate's {aspect}│
    │  Consider all eval   │
    │  data..."            │
    └────────┬─────────────┘
             │
             ▼
    ┌────────────────────────┐
    │  Philosopher           │
    │  process_message()     │
    └────────┬───────────────┘
             │
             ▼
    ┌────────────────────────┐
    │ Детальный анализ:      │
    │ - Глубинные инсайты    │
    │ - Скрытые паттерны     │
    │ - Риски и возможности  │
    │ - Рекомендации         │
    └────────────────────────┘
```

**Промпт**: См. PROMPTS_DOCUMENTATION.md → 4.4.3

**Передача данных**:
```python
input: aspect (choice from list)
output: deep_analysis (str)
```

---

### 3.5 Custom Assessment

**Назначение**: Создание индивидуального ассесмента для кандидата

**ASCII схема**:
```
┌────────────────────────────────────────────────────────┐
│         ПАЙПЛАЙН: CUSTOM ASSESSMENT                    │
└────────────────────────────────────────────────────────┘

    Пользователь выбирает тип:
    ┌───────────────────────────┐
    │ - Technical Challenge     │
    │ - Community Scenario      │
    │ - Leadership Exercise     │
    │ - Innovation Task         │
    └────────┬──────────────────┘
             │
             ▼
    ┌──────────────────────┐
    │ Формирование промпта:│
    │ "Create custom       │
    │  {assessment_type}   │
    │  for {candidate},    │
    │  tailored to their   │
    │  background..."      │
    └────────┬─────────────┘
             │
             ▼
    ┌────────────────────────┐
    │  Prophet               │
    │  process_message()     │
    └────────┬───────────────┘
             │
             ▼
    ┌────────────────────────┐
    │ Кастомный ассесмент:   │
    │ - Описание задачи      │
    │ - Критерии оценки      │
    │ - Временные рамки      │
    │ - Ожидаемые результаты │
    └────────────────────────┘
```

**Промпт**: См. PROMPTS_DOCUMENTATION.md → 4.4.4

**Передача данных**:
```python
input: assessment_type (choice from list), candidate_name (str)
output: custom_assessment (str)
```

---

### 3.6 Team Interaction Simulation

**Назначение**: Симуляция взаимодействия кандидата с командой

**ASCII схема**:
```
┌────────────────────────────────────────────────────────┐
│        ПАЙПЛАЙН: TEAM INTERACTION SIMULATION           │
└────────────────────────────────────────────────────────┘

    Пользователь выбирает сценарий:
    ┌───────────────────────────────┐
    │ - Discord Crisis Management   │
    │ - Community Event Planning    │
    │ - Team Collaboration Project  │
    │ - Technical Implementation    │
    │ - Community Feedback Session  │
    └────────┬──────────────────────┘
             │
             ▼
    ┌──────────────────────┐
    │ Формирование промпта:│
    │ "Simulate detailed   │
    │  team interaction    │
    │  scenario for {name} │
    │  as Discord Architect│
    │                      │
    │  Include:            │
    │  - Situation details │
    │  - Likely responses  │
    │  - Team dynamics     │
    │  - Decision process  │
    │  - Comm style        │
    │  - Challenges        │
    └────────┬─────────────┘
             │
             ▼
    ┌────────────────────────┐
    │  Prophet               │
    │  process_message()     │
    └────────┬───────────────┘
             │
             ▼
    ┌────────────────────────┐
    │ Симуляция:             │
    │ - Описание сценария    │
    │ - Диалоги              │
    │ - Реакции кандидата    │
    │ - Командная динамика   │
    │ - Анализ коммуникации  │
    │ - Решения и вызовы     │
    └────────────────────────┘
```

**Промпт**: См. PROMPTS_DOCUMENTATION.md → 4.4.6

**Передача данных**:
```python
input: scenario (choice), candidate_name (str)
output: interaction_simulation (str)
```

---

### 3.7 Growth Roadmap

**Назначение**: Создание персонализированной дорожной карты развития

**ASCII схема**:
```
┌────────────────────────────────────────────────────────┐
│            ПАЙПЛАЙН: GROWTH ROADMAP                    │
└────────────────────────────────────────────────────────┘

    Пользователь выбирает timeframe:
    ┌───────────────────┐
    │ - First 30 Days   │
    │ - 90 Day Plan     │
    │ - 6 Month Vision  │
    │ - 1 Year Dev      │
    └────────┬──────────┘
             │
             ▼
    ┌──────────────────────┐
    │ Формирование промпта:│
    │ "Create detailed     │
    │  growth roadmap for  │
    │  {name}...           │
    │                      │
    │  Include:            │
    │  - Milestones        │
    │  - Skill goals       │
    │  - Community targets │
    │  - Tech learning     │
    │  - Leadership dev    │
    │  - Success metrics   │
    └────────┬─────────────┘
             │
             ▼
    ┌────────────────────────┐
    │  Philosopher           │
    │  process_message()     │
    └────────┬───────────────┘
             │
             ▼
    ┌────────────────────────┐
    │ Дорожная карта:        │
    │ ┌──────────────────┐   │
    │ │ Milestone 1      │   │
    │ │ - Tasks          │   │
    │ │ - Skills         │   │
    │ │ - Metrics        │   │
    │ └──────────────────┘   │
    │ ┌──────────────────┐   │
    │ │ Milestone 2...   │   │
    │ └──────────────────┘   │
    └────────────────────────┘
```

**Промпт**: См. PROMPTS_DOCUMENTATION.md → 4.4.7

**Передача данных**:
```python
input: timeframe (choice), candidate_name (str)
output: growth_roadmap (str, markdown format)
```

---

### 3.8 Future Impact Analysis

**Назначение**: Анализ потенциального влияния кандидата на организацию

**ASCII схема**:
```
┌────────────────────────────────────────────────────────┐
│         ПАЙПЛАЙН: FUTURE IMPACT ANALYSIS               │
└────────────────────────────────────────────────────────┘

    Пользователь выбирает область:
    ┌────────────────────┐
    │ - Community Growth │
    │ - Tech Innovation  │
    │ - Team Culture     │
    │ - Educational      │
    │ - Platform Evol    │
    └────────┬───────────┘
             │
             ▼
    ┌──────────────────────┐
    │ Формирование промпта:│
    │ "Analyze potential   │
    │  future impact of    │
    │  {name} on PN:       │
    │                      │
    │  Consider:           │
    │  - Short-term wins   │
    │  - Medium-term ach   │
    │  - Long-term transf  │
    │  - Ripple effects    │
    │  - Innovations       │
    │  - Risks & opps      │
    └────────┬─────────────┘
             │
             ▼
    ┌────────────────────────┐
    │  Prophet               │
    │  process_message()     │
    └────────┬───────────────┘
             │
             ▼
    ┌────────────────────────┐
    │ Анализ влияния:        │
    │ ┌──────────────────┐   │
    │ │ 1-3 месяца       │   │
    │ │ Quick wins       │   │
    │ └──────────────────┘   │
    │ ┌──────────────────┐   │
    │ │ 3-6 месяцев      │   │
    │ │ Achievements     │   │
    │ └──────────────────┘   │
    │ ┌──────────────────┐   │
    │ │ 6-12 месяцев     │   │
    │ │ Transformation   │   │
    │ └──────────────────┘   │
    │ Risks & Opportunities  │
    └────────────────────────┘
```

**Промпт**: См. PROMPTS_DOCUMENTATION.md → 4.4.8

**Передача данных**:
```python
input: impact_area (choice), candidate_name (str)
output: future_impact_analysis (str)
```

---

### 3.9 Competitive Analysis

**Назначение**: Сравнение кандидата с рыночными стандартами

**ASCII схема**:
```
┌────────────────────────────────────────────────────────┐
│          ПАЙПЛАЙН: COMPETITIVE ANALYSIS                │
└────────────────────────────────────────────────────────┘

    Пользователь выбирает аспект:
    ┌───────────────────────────┐
    │ - Technical Skills        │
    │ - Community Building Exp  │
    │ - Innovation Capability   │
    │ - Leadership Potential    │
    │ - Market Value            │
    └────────┬──────────────────┘
             │
             ▼
    ┌──────────────────────┐
    │ Формирование промпта:│
    │ "Perform competitive │
    │  analysis of {name}  │
    │  against market...   │
    │                      │
    │  Include:            │
    │  - Benchmarks        │
    │  - Differentiators   │
    │  - Market position   │
    │  - Advantages        │
    │  - Value prop        │
    └────────┬─────────────┘
             │
             ▼
    ┌────────────────────────┐
    │  Philosopher           │
    │  process_message()     │
    └────────┬───────────────┘
             │
             ▼
    ┌────────────────────────┐
    │ Конкурентный анализ:   │
    │ ┌──────────────────┐   │
    │ │ Market Benchmark │   │
    │ │ ■■■■■■□□ 75%     │   │
    │ └──────────────────┘   │
    │ ┌──────────────────┐   │
    │ │ Candidate Score  │   │
    │ │ ■■■■■■■■■ 90%    │   │
    │ └──────────────────┘   │
    │ Unique Differentiators │
    │ Competitive Advantages │
    │ Market Alignment Gaps  │
    └────────────────────────┘
```

**Промпт**: См. PROMPTS_DOCUMENTATION.md → 4.4.9

**Передача данных**:
```python
input: aspect (choice), candidate_name (str)
output: competitive_analysis (str)
```

---

### 3.10 Suggest Improvements

**Назначение**: Предложения по улучшению процесса оценки

**ASCII схема**:
```
┌────────────────────────────────────────────────────────┐
│         ПАЙПЛАЙН: SUGGEST IMPROVEMENTS                 │
└────────────────────────────────────────────────────────┘

    Входные данные:
    - Профиль кандидата
    - Процесс оценки
      │
      ▼
    ┌──────────────────────┐
    │ Формирование промпта:│
    │ "Based on candidate  │
    │  profile and our     │
    │  evaluation process: │
    │                      │
    │  1. What could we    │
    │     improve?         │
    │  2. What additional  │
    │     aspects?         │
    │  3. How to better    │
    │     assess this type?│
    └────────┬─────────────┘
             │
             ▼
    ┌────────────────────────┐
    │  Philosopher           │
    │  process_message()     │
    └────────┬───────────────┘
             │
             ▼
    ┌────────────────────────┐
    │ Улучшения:             │
    │ - Process improvements │
    │ - Additional aspects   │
    │ - Better assessment    │
    │   methods              │
    │ - Meta-insights        │
    └────────────────────────┘
```

**Промпт**: См. PROMPTS_DOCUMENTATION.md → 4.4.5

**Передача данных**:
```python
input: candidate_profile (dict), evaluation_process (context)
output: improvement_suggestions (str)
```

---

### 3.11 Exit

**Назначение**: Выход из интерактивной сессии с подтверждением

**ASCII схема**:
```
┌────────────────────────────────────────┐
│        ПАЙПЛАЙН: EXIT                  │
└────────────────────────────────────────┘

    Пользователь выбирает Exit
      │
      ▼
    ┌──────────────────────┐
    │ Confirm.ask()        │
    │ "Are you sure you    │
    │  want to exit?"      │
    └────────┬─────────────┘
             │
             ├─ Yes → break loop → конец
             │
             └─ No → return to menu
```

---

### Сводная таблица интерактивных пайплайнов

| # | Название | Агент | Тип ввода | Промпт |
|---|----------|-------|-----------|--------|
| 1 | Chat | Both | Question (str) | 4.4.1 |
| 2 | Approve | - | Notes (str, opt) | - |
| 3 | Reject | - | Reason (str, req) | - |
| 4 | Alt Roles | Philosopher | - | 4.4.2 |
| 5 | Deep Dive | Philosopher | Aspect (choice) | 4.4.3 |
| 6 | Assessment | Prophet | Type (choice) | 4.4.4 |
| 7 | Team Sim | Prophet | Scenario (choice) | 4.4.6 |
| 8 | Roadmap | Philosopher | Timeframe (choice) | 4.4.7 |
| 9 | Impact | Prophet | Area (choice) | 4.4.8 |
| 10 | Competitive | Philosopher | Aspect (choice) | 4.4.9 |
| 11 | Improvements | Philosopher | - | 4.4.5 |
| 12 | Exit | - | Confirmation | - |

### Характеристики интерактивных пайплайнов

- **Режим**: Циклический (while True до exit)
- **Агенты**: Philosopher (7 пайплайнов), Prophet (4 пайплайна), None (3 пайплайна)
- **Ввод пользователя**: Требуется для большинства пайплайнов
- **Контекст**: Все пайплайны имеют доступ к исходной оценке кандидата
- **История**: Сохраняется в `chat_history` (только для Chat)
- **Временные затраты**: 3-15 секунд на запрос (зависит от сложности)

---

## 4. Технические детали

### 4.1 Общая архитектура системы

```
┌────────────────────────────────────────────────────────────┐
│                    АРХИТЕКТУРА СИСТЕМЫ                     │
└────────────────────────────────────────────────────────────┘

                      ┌─────────────────┐
                      │  CLI Interface  │
                      │   (Typer app)   │
                      └────────┬────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │  ApplicationProcessor   │
                  │  (CSV → dict)           │
                  └────────┬────────────────┘
                           │
                           ▼
                  ┌─────────────────────────┐
                  │      HRTeam             │
                  │  - TalentPhilosopher    │
                  │  - CandidateProphet     │
                  │  - conversation_history │
                  └────────┬────────────────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
              ▼            ▼            ▼
    ┌──────────────┐ ┌──────────┐ ┌──────────────┐
    │ Philosopher  │ │ Prophet  │ │ Interactive  │
    │   Agent      │ │  Agent   │ │   Session    │
    └──────┬───────┘ └────┬─────┘ └──────┬───────┘
           │              │               │
           └──────────────┼───────────────┘
                          │
                          ▼
                 ┌─────────────────┐
                 │  OpenAI GPT-4   │
                 │   (gpt-4o)      │
                 └─────────────────┘
```

### 4.2 Иерархия агентов

```
BaseAgent (src/agents/base_agent.py)
    │
    ├── TalentPhilosopher (src/agents/philosopher.py)
    │   ├── _get_system_prompt()
    │   ├── evaluate_candidate(application_data)
    │   └── generate_evaluation_report(evaluation_data)
    │
    ├── CandidateProphet (src/agents/prophet.py)
    │   ├── _get_system_prompt()
    │   ├── evaluate_candidate(application_data)
    │   └── generate_evaluation_report(evaluation_data)
    │
    ├── UserAdvocateAgent (src/agents/advocate.py)
    │   ├── _get_system_prompt()
    │   ├── introduce_case(user_input)
    │   ├── request_recommendations(strategist_analysis)
    │   ├── summarize_recommendations(recommendations)
    │   └── generate_report_section(topic, content)
    │
    └── StrategistAgent (src/agents/strategist.py)
        ├── _get_system_prompt()
        ├── analyze_case(user_input, advocate_intro)
        ├── provide_recommendations(advocate_request)
        └── generate_report_section(topic, content)
```

### 4.3 Поток данных между компонентами

```
┌──────────┐     ┌──────────────┐     ┌──────────────┐
│   CSV    │ --> │ Processor    │ --> │ application_ │
│   File   │     │ load_apps()  │     │    data      │
└──────────┘     └──────────────┘     └──────┬───────┘
                                              │
                  ┌───────────────────────────┘
                  │
                  ▼
         ┌────────────────────┐
         │   HRTeam           │
         │   evaluate_        │
         │   application()    │
         └────────┬───────────┘
                  │
        ┌─────────┴─────────┐
        │                   │
        ▼                   ▼
┌───────────────┐   ┌───────────────┐
│ Philosopher   │   │    Prophet    │
│ evaluate_     │   │   evaluate_   │
│ candidate()   │   │   candidate() │
└───────┬───────┘   └───────┬───────┘
        │                   │
        └─────────┬─────────┘
                  │
                  ▼
       ┌──────────────────────┐
       │ conversation_history │
       │ [(agent, response)]  │
       └──────────┬───────────┘
                  │
                  ▼
         ┌────────────────────┐
         │ generate_report()  │
         └────────┬───────────┘
                  │
                  ▼
         ┌────────────────────┐
         │ report_data (dict) │
         └────────┬───────────┘
                  │
                  ▼
       ┌────────────────────────┐
       │ InteractiveSession     │
       │ start_interactive_     │
       │ session()              │
       └────────────────────────┘
```

### 4.4 Сводная статистика пайплайнов

#### Основные пайплайны: 2
1. Оценка кандидатов (Philosopher + Prophet)
2. Карьерное консультирование (Advocate + Strategist)

#### Интерактивные пайплайны: 12
- Диалоговые: 2 (Chat, Improvements)
- Аналитические: 7 (Alt Roles, Deep Dive, Assessment, Team Sim, Roadmap, Impact, Competitive)
- Процедурные: 3 (Approve, Reject, Exit)

#### Используемые AI агенты: 4
1. **Talent Philosopher** - философская оценка, глубинный анализ
2. **Candidate Prophet** - пророческая оценка, видение будущего
3. **User Advocate** - карьерное консультирование, защита интересов
4. **Career Strategist** - стратегические рекомендации, контрарианское мышление

#### Общее количество AI промптов: 22+
- Системные промпты: 4
- Промпты оценки: 4
- Роль-специфичные: 2
- Интерактивные: 12+

### 4.5 Паттерны передачи данных

#### 1. Последовательная обработка
```
Input → Agent 1 → Output 1 → Agent 2 → Output 2 → Final Result
```
Используется в: Оценка кандидатов, Карьерное консультирование

#### 2. Параллельная обработка (концептуально)
```
        ┌─→ Agent 1 → Output 1 ─┐
Input ──┤                        ├─→ Merge → Final Result
        └─→ Agent 2 → Output 2 ─┘
```
Используется в: Chat with Principals (оба агента отвечают независимо)

#### 3. Циклическая обработка
```
Input → Agent → Output → User Input → Agent → Output → ...
```
Используется в: Интерактивные сессии

### 4.6 Временные характеристики

| Пайплайн | Среднее время | Агентов | Вызовов AI |
|----------|---------------|---------|------------|
| Оценка кандидатов | ~20-30 сек | 2 | 2 |
| Карьерное консультирование | ~25-35 сек | 2 | 5 |
| Chat | ~8-12 сек | 2 | 2 |
| Deep Dive | ~5-10 сек | 1 | 1 |
| Roadmap | ~8-15 сек | 1 | 1 |
| Team Simulation | ~10-15 сек | 1 | 1 |
| Approve/Reject | <1 сек | 0 | 0 |

### 4.7 Форматы данных

#### Application Data (входные данные)
```python
{
    'name': str,
    'role': str,
    'application': str,  # Полный текст заявки
    'background': str,   # Дополнительная информация
    # ... другие поля из CSV
}
```

#### Conversation History
```python
conversation_history = [
    ("philosopher", "Philosophical analysis text..."),
    ("prophet", "Prophetic vision text..."),
    # ...
]
```

#### Report Data
```python
{
    'scores': {
        'category': {
            'subcategory': float,  # 0-10
            'overall': float
        }
    },
    'total_score': float,
    'recommendation': str,
    'strengths': {
        'category': [str]
    },
    'development_areas': {
        'category': [str]
    }
}
```

### 4.8 Конфигурация и настройки

#### AI модель
- **Модель**: OpenAI GPT-4 (gpt-4o)
- **Температура**: ~0.7-0.8 (для креативных ответов)
- **Max tokens**: Динамическое (зависит от промпта)

#### Файловая структура
```
HR-Principals/
├── src/
│   ├── agents/
│   │   ├── base_agent.py
│   │   ├── philosopher.py
│   │   ├── prophet.py
│   │   ├── advocate.py
│   │   └── strategist.py
│   ├── utils/
│   │   ├── data_processor.py
│   │   ├── ui_manager.py
│   │   ├── visualizer.py
│   │   └── prompt_loader.py
│   └── main.py
├── prompts/
│   ├── talent_philosopher.yaml
│   ├── candidate_prophet.yaml
│   └── roles/
│       └── discord_architect.yaml
└── data/
    └── applications.csv
```

### 4.9 Ключевые зависимости

- `openai` - API для GPT-4
- `rich` - UI и форматирование вывода
- `typer` - CLI interface
- `asyncio` - Асинхронная обработка
- `pydantic` - Валидация данных (если используется)
- `pyyaml` - Загрузка конфигурации промптов

---

## Заключение

### Основные преимущества архитектуры

1. **Модульность** - каждый агент независим и может быть заменен
2. **Расширяемость** - легко добавить новые пайплайны и агентов
3. **Прозрачность** - четкая трассировка данных между этапами
4. **Интерактивность** - 12 различных способов взаимодействия с оценкой
5. **Философский подход** - уникальная методология оценки через диалог агентов

### Рекомендации по использованию

1. **Для оценки кандидатов**: Используйте основной пайплайн оценки, затем углубляйтесь через интерактивные опции
2. **Для карьерного консультирования**: Запускайте диалог Advocate-Strategist для нестандартных карьерных советов
3. **Для анализа**: Используйте Deep Dive, Competitive Analysis и Future Impact для детального исследования
4. **Для принятия решений**: Комбинируйте несколько интерактивных пайплайнов для всесторонней картины

### Связь с PROMPTS_DOCUMENTATION.md

Все промпты, используемые в пайплайнах, детально задокументированы в файле `PROMPTS_DOCUMENTATION.md`. Для каждого пайплайна указаны ссылки на соответствующие промпты.

---

**Документация создана:** 2025-11-11
**Версия приложения:** HR-Principals Multi-Agent AI Recruitment System
**Общее количество пайплайнов:** 14 (2 основных + 12 интерактивных)
**AI агентов:** 4 (Philosopher, Prophet, Advocate, Strategist)
**AI промптов:** 22+

