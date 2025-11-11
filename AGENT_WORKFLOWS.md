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

