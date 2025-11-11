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

