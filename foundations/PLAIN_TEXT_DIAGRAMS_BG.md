# PlainText Diagrams — архив от основополагащия разговор

## Статус

Този файл пази PlainText (обикновен текст) схемите и визуалните модели, възникнали в основополагащия разговор.

Целта не е литературна редакция, а **запазване на визуалното мислене** за бъдещи slides (слайдове), упражнения и преподавателски материали.

## 1. Общ слой на agentic systems (агентните системи)

```text
APPLICATION
    │
WORKFLOW
    │
AGENT
    │
RUNTIME / ORCHESTRATOR
    │
    ├── TOOLS
    ├── MEMORY / STATE
    └── MODELS
         │
     MCP / APIs / SDKs
         │
   EXTERNAL WORLD
```

## 2. Минималният agent loop (цикъл на агента)

```text
Goal
 ↓
Observe current state
 ↓
Decide what to do
 ↓
Take action
 ↓
Observe result
 ↓
Decide again
 ↓
...
 ↓
Goal achieved / stop
```

## 3. Agent срещу Tool

```text
Agent = решава какво да прави

Tool = прави нещо
```

## 4. Достъп без MCP

```text
Agent
 ├── custom Gmail integration
 ├── custom PostgreSQL integration
 ├── custom GitHub integration
 └── custom filesystem integration
```

## 5. Достъп чрез MCP

```text
Agent
   │
  MCP
   │
   ├── Gmail Server
   ├── GitHub Server
   ├── Database Server
   └── Files Server
```

## 6. Runtime / Orchestrator

```text
Agent started
      ↓
load state
      ↓
call model
      ↓
model requests tool
      ↓
execute tool
      ↓
save state
      ↓
call model again
      ↓
pause for human
      ↓
resume tomorrow
```

## 7. Workflow срещу Agent

```text
Workflow:
A → B → C → D

Agent:
A
↓
LLM решава
↓
може B
може C
може D
може пак A
```

## 8. n8n с agentic island (агентен остров)

```text
Webhook
 ↓
Agent
 ├─ решава кой tool
 ├─ решава дали да търси
 ├─ решава дали да повтори
 └─ връща резултат
 ↓
Continue workflow
```

```text
deterministic workflow
        +
agentic islands
```

## 9. Deterministic where possible, agentic where useful

```text
receive invoice
      ↓
validate MIME        ← deterministic
      ↓
extract PDF          ← deterministic
      ↓
understand content   ← AI
      ↓
confidence < 80%?    ← deterministic
      ↓
human review         ← deterministic workflow
```

## 10. Skill (умение) срещу Tool (инструмент)

```text
Tool:
search_web()

Skill:
Competitive Research

instructions:
1. search official sources
2. search news
3. compare claims
4. cite evidence

tools:
- search_web
- browser
- database
```

## 11. Обобщена карта на понятията

```text
MODEL
мисли / генерира

AGENT
преследва цел

SKILL
знае как се изпълнява определен тип задача

TOOL
извършва конкретно действие

MCP
стандартизира достъпа до tools/resources

RUNTIME / ORCHESTRATOR
управлява изпълнението, state, loops, retries, pause/resume

WORKFLOW
определя процеса

n8n
workflow-centric orchestrator

LangGraph
agent-centric orchestrator/runtime
```

## 12. Cloud или local LLM

```text
Agent
  │
  ├─ cloud LLM
  │    ├─ OpenAI
  │    ├─ Anthropic
  │    └─ Google
  │
  └─ local LLM
       ├─ Llama
       ├─ Qwen
       ├─ Mistral
       └─ Gemma
```

```text
Agent
  │
  ├─ local LLM → класификация, routing, extraction
  │
  └─ cloud LLM → сложен reasoning и трудни решения
```

## 13. Нашият Human-in-the-loop scaffolded LLM workflow

```text
.md файлове в repository (хранилище)
        ↓
правила / процедури / контекст / решения
        ↓
User (човекът)
        ↓
ChatGPT / LLM (голям езиков модел)
        ↓
reasoning (разсъждение)
        ↓
конкретна задача
        ↓
резултат
        ↓
човекът решава какво следва
```

## 14. Workflow specification чрез Markdown

```text
DISSERTATION_WORKFLOW.md

1. Прочети текущия раздел
2. Провери източниците
3. Провери аргументацията
4. Отбележи слабите места
5. Предложи корекции
6. Изчакай одобрение
7. Продължи
```

## 15. Човекът като orchestrator

```text
Goal
 ↓
ти казваш какво правим
 ↓
аз чета правилата
 ↓
аз изпълнявам
 ↓
ти проверяваш
 ↓
ти казваш какво следва
```

## 16. Agent runtime

```text
Goal
 ↓
LLM decides next action
 ↓
execute action
 ↓
observe result
 ↓
update state
 ↓
decide next action
 ↓
...
```

## 17. Еволюция към agent

```text
Prompt
 ↓
Prompt + правила
 ↓
Prompt + правила + repository (хранилище)
 ↓
Workflow definition (описание на процес)
 ↓
Skill (умение)
 ↓
Agent (агент)
 ↓
Agent Runtime (среда за изпълнение на агента)
```

```text
Prompt
   ↓
Externalized rules (изнесени правила)
   ↓
Repository-backed workflow
   ↓
Human orchestration
   ↓
LLM execution
```

## 18. Shared control (споделен контрол)

```text
Спас
 │
 ├─ определя целта
 ├─ задава правилата
 ├─ одобрява решения
 ├─ спира / коригира
 │
 ▼
LLM
 │
 ├─ анализира
 ├─ предлага
 ├─ структурира
 └─ изпълнява интелектуалната работа
```

## 19. Prompt programming

```text
НЕ пишем:

if source_missing:
    stop()

а пишем:

"Ако липсва критичен източник,
не прави заключение.
Кажи какво липсва."
```

## 20. Deterministic shell, bounded agentic core

```text
Потребител
    ↓
Детерминистичен код
    ├─ кой има право
    ├─ кои инструменти са разрешени
    ├─ какви данни могат да се четат
    ├─ какви действия могат да се извършват
    ├─ лимити
    ├─ валидиране
    └─ кога е необходимо човешко одобрение
              ↓
             Agent (агент)
              ↓
       "Как да постигна целта?"
              ↓
       избира допустимо действие
              ↓
       Детерминистична проверка
              ↓
       Tool (инструмент)
```

## 21. Проверка преди write action (действие за запис)

```text
LLM решение:
"Искам да изпратя този e-mail."

        ↓

КОД:
Има ли право?
Към разрешен получател ли е?
Съдържа ли защитени данни?
Изисква ли human approval (човешко одобрение)?
Надвишава ли risk threshold (праг на риска)?

        ↓

ДА → изпълнение
НЕ → отказ
```

## 22. Етапи на делегиране

```text
ЕТАП 1

Human (човек)
   ↓
правила в .md
   ↓
LLM
   ↓
Human решава следващата стъпка
```

```text
ЕТАП 2

Human
   ↓
правила
   ↓
Workflow engine (система за изпълнение на работни процеси)
   ↓
LLM
   ↓
Human approval при определени точки
```

```text
ЕТАП 3

Human задава:
  Goal (цел)
  Policies (правила)
  Boundaries (граници)

        ↓

Agent Runtime (среда за изпълнение на агента)

        ↓

Agent сам решава:
  какво да провери
  кой разрешен tool да използва
  дали му трябва още информация
  дали да повтори дадена стъпка
  кога задачата е изпълнена

        ↓

Code-enforced guardrails
(наложени чрез код защитни ограничения)

        ↓

Tools / external systems
(инструменти / външни системи)
```

## 23. Soft срещу Hard Constraint

```text
Soft:
"Не изпращай e-mail без мое разрешение."

Hard:
if action == SEND_EMAIL:
    require_human_approval()
```

## 24. Класификация на правилата

```text
Правило
  │
  ├─ поведенческо
  │      ↓
  │   instruction (инструкция)
  │
  ├─ процесно
  │      ↓
  │   workflow logic (логика на работния процес)
  │
  └─ security-critical (критично за сигурността)
         ↓
      код / policy engine
      (система за налагане на правила)
```

## 25. Архитектурен модел на AI agent

```text
                   Human (човек)
                        │
                 Goal + Policies
                 (цел + правила)
                        │
                        ▼
                 ┌─────────────┐
                 │   AGENT     │
                 │   (агент)   │
                 │             │
                 │ Model       │
                 │ State       │
                 │ Reasoning   │
                 └──────┬──────┘
                        │
                chooses action
                (избира действие)
                        │
                        ▼
                Guardrails
          (защитни ограничения)
                        │
                        ▼
                 Tools
              (инструменти)
                        │
                        ▼
              Environment
                 (среда)
                        │
                        └──── feedback
                           (обратна връзка)
```

## 26. Не е агент / вече е агент

```text
Prompt → LLM → Answer
```

```text
A → B → C → D
```

```text
Goal
 ↓
LLM решава какво е нужно
 ↓
Tool A
 ↓
резултат
 ↓
LLM решава, че не стига
 ↓
Tool C
 ↓
резултат
 ↓
LLM преценява, че целта е постигната
 ↓
Stop
```

## 27. Autonomy spectrum (спектър на автономността)

```text
ниска автономност ───────────────────── висока автономност

chatbot     guided agent        bounded agent       autonomous agent
(чатбот)    (воден агент)       (ограничен агент)   (автономен агент)
```

## 28. Learning workflow (учебен процес)

```text
1. Software thinking
   (софтуерно мислене)

2. Deterministic workflow
   (детерминистичен работен процес)

3. Tools + APIs + Identity
   (инструменти + програмни интерфейси + идентичност)

4. LLM integration
   (интегриране на голям езиков модел)

5. Agent loop
   (цикъл на агента)

6. Guardrails + Trust Boundaries
   (защитни ограничения + граници на доверие)

7. Testing + Observability
   (тестване + наблюдаемост)

8. Frameworks / n8n / LangGraph
   (рамки и платформи)
```

## 29. Детерминистичен software workflow

```text
Input
 ↓
Validate
 ↓
Process
 ↓
Decision
 ↓
Action
 ↓
Log
```

## 30. Agent към external world (външния свят)

```text
Agent
  ↓
Tool
(инструмент)
  ↓
API / MCP
(програмен интерфейс / протокол за контекст на модела)
  ↓
External system
(външна система)
```

## 31. Правата не са просто „връзка към услуга“

```text
може да чете email     → READ
може да изпраща email  → WRITE

Това НЕ са едно и също право.
```

## 32. LLM в workflow без agent

```text
Input
 ↓
LLM
 ↓
Classification
(класификация)
 ↓
Deterministic workflow
(детерминистичен процес)
```

## 33. Първият agent loop

```text
Goal
 ↓
Observe
 ↓
Decide
 ↓
Tool
 ↓
Observe
 └────→ Decide again
```

## 34. Автономен избор на следващо действие

```text
Goal:
"Установи какъв е проблемът
и предложи решение."

        ↓

Agent
 ├─ Search KB?
 ├─ Query DB?
 ├─ Ask user?
 ├─ Check status?
 └─ Stop?
```

## 35. Guardrails започват от blast radius

```text
Каква автономност даваме?
        ↓
Какъв е blast radius
(потенциалният обхват на вредата)?
        ↓
Какви ограничения са нужни?
```

## 36. Authorization извън LLM

```text
Agent:
"Искам да изтрия customer record
(клиентски запис)."

        ↓

НЕ питаме LLM:
"Сигурен ли си?"

        ↓

Policy / Code
(правило / код):
НЯМАШ ПРАВО.

        ↓

Denied
(отказано)
```

## 37. Unknown unknowns (неизвестните неизвестни)

```text
shared credential
(споделени удостоверителни данни)

overprivileged token
(токен с прекомерни права)

missing authorization
(липсваща оторизация)

race condition
(състезателно условие)

unbounded retry
(неограничени повторни опити)

prompt injection path
(път за инжектиране на инструкции)

data leakage
(изтичане на данни)

missing audit trail
(липса на одитна следа)

unsafe failure mode
(опасно поведение при отказ)
```

## 38. Работещ код + лоша архитектура

```text
лоша архитектура
      +
работещ код
      +
автономен агент
      +
реални credentials
(удостоверителни данни)
      +
реални tools
(инструменти)

→ системата работи прекрасно...

...докато не направи нещо прекрасно грешно.
```

## 39. Маркетинговият learning path

```text
n8n
 ↓
drag & drop
 ↓
AI Agent
 ↓
готово!
🎉
```

## 40. Архитектурният learning path

```text
Problem
(проблем)
 ↓
Architecture
(архитектура)
 ↓
Trust model
(модел на доверие)
 ↓
Deterministic workflow
(детерминистичен процес)
 ↓
Security boundaries
(граници за сигурност)
 ↓
LLM
 ↓
Controlled autonomy
(контролирана автономност)
 ↓
Agent
 ↓
Framework / GUI
(рамка / графичен интерфейс)
```

## 41. Ритъм на модул

```text
~ 1 академичен час теория
~ 2 академични часа лабораторно упражнение
~ 1 академичен час анализ / discussion / review
```

## 42. Финален проект

```text
1. Goal
2. Architecture
3. Trust boundaries
4. Tools
5. Identity / permissions
6. Deterministic workflow
7. Agentic decisions
8. Guardrails
9. Human approval points
10. Failure modes
11. Tests
12. Working prototype
```

## 43. Основна позиция за курса

```text
n8n трябва да бъде лабораторията,
не учебната програма.
```
