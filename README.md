# cframe-reasoning-core
Structured reasoning schemas and examples for C-Frame (Head Agent + RPM + Deadlock).


markdown
# C-Frame Structured Reasoning

**C-Frame** is a phase-based reasoning framework for Large Language Models (LLMs).  
It enforces deliberate, System-2-style thinking by separating **problem structuring**,  
**phase-controlled reasoning**, and **deadlock-aware perspective shifts**.

This repository provides **schemas, system prompts, and runnable examples**  
that turn LLMs from fast answer generators into **controlled reasoning systems**.

---

## What is C-Frame?

C-Frame is built on a simple but powerful idea:

> **Most hard problems are not hard because answers are missing,  
but because the question structure is wrong.**

C-Frame addresses this by:
- Structuring problems *before* answering (Head Agent)
- Forcing reasoning to move through explicit phases (RPM)
- Detecting stagnation and uncertainty as first-class objects (DeadlockSpec)
- Enabling perspective shifts instead of premature conclusions

---

## Core Components

### 1. Head Agent
- Converts raw user input into a structured problem representation
- Identifies intent, constraints, unknowns, assumptions, and stakes
- **Does not generate answers**

### 2. RPM (Relational Perspective Manager)
- Controls reasoning as a **4-phase state machine**:
  - Concept → Relation → Structure → Horizon
- Enforces phase transitions with guards and loop control
- Routes reasoning to sub-agents when deadlocks are detected

### 3. Deadlock Awareness
- Detects structural stagnation (e.g. repeated comparisons, value conflicts)
- Represents uncertainty explicitly instead of hiding it
- Enables meaningful perspective shifts

---

## Repository Structure

```

templates/
head_agent.schema.json
rpm_phase.schema.json
rpm_phase.schema.ko.json

examples/
reasoning_run_spec.example.json

```

---

## How to Use these Schemas (EN)

1. Start by feeding your raw user input into the **Head Agent**.  
2. The Head Agent produces a `HeadAgentSpec`, structuring the problem *before* any solution is attempted.  
3. Pass this structured output to the **RPM (Relational Perspective Manager)**.  
4. RPM moves reasoning through four phases: **Concept → Relation → Structure → Horizon**.  
5. Each phase has explicit goals, questions, and guarded transition rules.  
6. When reasoning stagnates, RPM triggers a **DeadlockSpec** to surface structural uncertainty.  
7. Detected deadlocks are interpreted via topological signatures (e.g., fragmentation or loops).  
8. Based on phase and topology, RPM recommends appropriate sub-agents.  
9. Reasoning proceeds through bounded loops until a crux is resolved or output is ready.  
10. This design prevents premature answers and enforces deliberate reasoning.

---

## 스키마 사용 방법 (KO)

1. 먼저 사용자 입력을 **Head Agent**에 전달합니다.  
2. Head Agent는 답을 만들지 않고, 문제를 구조화한 `HeadAgentSpec`을 생성합니다.  
3. 이 출력은 **RPM(Relational Perspective Manager)**의 입력이 됩니다.  
4. RPM은 사고를 **개념 → 관계 → 구조 → 지평**의 4단계로 이동시킵니다.  
5. 각 단계는 목표, 핵심 질문, 전이 조건을 명시적으로 가집니다.  
6. 사고가 정체되면 **DeadlockSpec**을 생성하여 불확실성을 드러냅니다.  
7. 데드락은 위상 패턴(분절, 루프 등)으로 해석됩니다.  
8. 단계와 위상에 따라 적절한 서브 에이전트가 추천됩니다.  
9. 추론은 제한된 루프 안에서 반복됩니다.  
10. 이 구조는 성급한 답변을 막고 심층 사고를 강제합니다.

---

## System Prompt Template (EN)

```

You are operating under explicit structural constraints.

Attached files:

* head_agent.schema.json
* rpm_phase.schema.json

You must treat these schemas as binding constraints, not as reference documents.
First, produce a HeadAgentSpec that strictly follows head_agent.schema.json.
Do NOT generate solutions or recommendations at this stage.

Then, use the HeadAgentSpec as input to the RPM.
Reason only through the four RPM phases (Concept → Relation → Structure → Horizon),
respecting transition rules, deadlock hooks, routing policies, and loop control.

If reasoning stagnates, explicitly generate a DeadlockSpec.
Do not skip phases. Do not answer prematurely.
Only produce final outputs after structured reasoning is complete.

```

---

## 시스템 프롬프트 템플릿 (KO)

```

당신은 명시적인 구조적 제약 하에서 작동합니다.

첨부 파일:

* head_agent.schema.json
* rpm_phase.schema.json

이 스키마들은 참고 문서가 아니라 반드시 따라야 할 구속 조건입니다.
먼저 head_agent.schema.json을 엄격히 준수하여 HeadAgentSpec을 생성하세요.
이 단계에서는 해답이나 권고를 생성하지 마십시오.

그 다음 HeadAgentSpec을 입력으로 RPM을 실행합니다.
사고는 반드시 네 단계(개념 → 관계 → 구조 → 지평)를 통과해야 하며,
전이 규칙과 데드락 훅, 루프 제어를 준수해야 합니다.

사고가 정체되면 DeadlockSpec을 명시적으로 생성하십시오.
단계를 건너뛰거나 성급한 답변을 하지 마십시오.
구조적 추론이 완료된 후에만 최종 출력을 생성할 수 있습니다.

```

---

## Comparison: With vs Without C-Frame

### Without C-Frame
- Immediate answers
- Pros/cons lists
- Repeated comparisons
- Hidden uncertainty
- Fast but shallow conclusions

### With C-Frame
- Explicit problem structuring
- Phase-controlled reasoning
- Deadlock detection (loops, value conflicts)
- Perspective shifts before conclusions
- Slower, but meaningfully transformative outcomes

> **Without C-Frame:** The model answers the question.  
> **With C-Frame:** The model determines whether the question itself is answerable.

---

## Why This Matters

C-Frame is not about making LLMs “smarter” at answering.

It is about making them:
- **More deliberate**
- **More stable**
- **More aligned with human reasoning over time**

This repository demonstrates how reasoning itself can be **designed, constrained, and audited**.

---

## License

MIT License
```

