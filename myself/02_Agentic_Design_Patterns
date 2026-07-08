# Week 1 - Day 2: Agentic Design Patterns

## Overview

In the blog **"Building Effective Agents"**, Anthropic introduced several common architectural patterns for building AI systems.

These are **not strict rules** or official standards. Instead, they are reusable ideas that help engineers structure AI applications effectively. Real-world systems often combine multiple patterns rather than following a single one.

Anthropic identifies:

-   **5 Workflow Design Patterns**
-   **1 Agent Pattern**

* * *

# Important Note

Unlike traditional software engineering design patterns (such as Factory, Singleton, or Strategy), AI design patterns are **guidelines**, not rigid architectures.

Key points:

-   Multiple patterns can be combined.
-   Real-world implementations rarely match the diagrams exactly.
-   Choose patterns based on the problem being solved.
-   Focus on understanding the concepts rather than memorizing the names.

* * *

# 1\. Prompt Chaining

## Definition

Prompt chaining breaks a large task into a sequence of smaller LLM calls, where the output of one prompt becomes the input of the next.

### Workflow

```
Input   │   -> LLM 1   │   -> Gate   │   ->LLM 2   │   ->LLM 3   │   ▼Output
```

Application code may optionally include decision points between the prompts. Like `Gate` mentioned ib the diagram

* * *

## Purpose

Instead of asking one enormous prompt, solve the problem step by step.

Typical uses include:

-   Multi-step reasoning
-   Data extraction followed by summarization
-   Planning followed by execution
-   Document analysis pipelines

* * *

## Example

Suppose a user uploads a research paper.

Instead of asking one prompt:

> "Read this paper and summarize everything."

The application performs:

1.  Extract important sections.
2.  Summarize each section.
3.  Generate a final summary.

Each stage is handled by a separate LLM call.

* * *

## Advantages

-   Easier debugging
-   Better prompt specialization
-   More reliable outputs
-   Simpler maintenance

* * *

# 2\. Routing

## Definition

Routing uses an LLM to determine **which specialized workflow or model should handle a request**.

### Workflow

```
            User Request
                 │
                 ▼
           Router LLM
          /     |      \
         ▼      ▼       ▼
 Technical  Business   Other
     │          │        │
     ▼          ▼        ▼
 Specialized Specialized Specialized
     LLM         LLM         LLM
```

The router classifies the request and forwards it to the most appropriate prompt or workflow.

* * *

## Purpose

Separate responsibilities across specialized prompts.

* * *

## Example

A customer support chatbot receives:

> "My payment failed."

The router determines that this is a **billing issue** and forwards it to a billing assistant rather than a technical support assistant.

Possible routes:

-   Technical Support
-   Billing
-   Sales
-   General Questions

Each specialized assistant contains only the knowledge relevant to its domain.

* * *

## Advantages

-   Better accuracy
-   Smaller prompts
-   Easier maintenance
-   Separation of concerns

* * *

# 3\. Parallelization

## Definition

Independent subtasks are executed simultaneously using multiple LLM calls.

### Workflow

```
          Input
            │
            ▼
   Application Code
     /      |      \
    ▼       ▼       ▼
 LLM 1   LLM 2   LLM 3
    \       |      /
     ▼      ▼     ▼
     Aggregation(Application code)
         │
         ▼
       Output
```

Unlike prompt chaining, these tasks do not depend on one another.

* * *

## Purpose

Reduce execution time by processing independent tasks concurrently.

* * *

## Example

A resume analysis system needs to evaluate:

-   Skills
-   Experience
-   Education

Each category can be analyzed independently, then merged into one report.

* * *

## Advantages

-   Faster execution
-   Better scalability
-   Independent task execution

* * *

# 4\. Orchestrator–Worker Pattern

## Definition

An LLM dynamically decides how to divide a complex task into smaller tasks, assigns them to workers, and another LLM combines the results.

### Workflow

```
             Input
               │
               ▼
      Orchestrator LLM
        /      |      \
       ▼       ▼       ▼
    Worker   Worker   Worker
      LLM      LLM      LLM
        \       |       /
         ▼      ▼      ▼
      Synthesizer LLM
             │
             ▼
           Output
```

* * *

## Difference from Parallelization

### Parallelization

Application code determines:

-   Number of tasks
-   Task boundaries
-   Task assignments

### Orchestrator–Worker

The **LLM itself** decides: Orchestrator and Synthesizer are LLM not application code

-   How to break the task apart
-   How many workers are required
-   What each worker should do
-   How to combine the results

* * *

## Example

User request:

> "Create a market analysis report."

The orchestrator decides:

-   Worker 1 → Analyze competitors
-   Worker 2 → Analyze pricing
-   Worker 3 → Analyze customer sentiment

A synthesizer LLM then combines these into a final report.

* * *

## Advantages

-   Flexible decomposition
-   Dynamic planning
-   Handles complex tasks efficiently

* * *

# 5\. Evaluator–Optimizer

## Definition

One LLM generates a solution, while another LLM evaluates its quality.

If the evaluator rejects the output, the generator tries again.

### Workflow

```
Generator LLM
      │
      ▼
Evaluator LLM
   │       │
Reject   Accept
   │        │
   ▼        ▼
Retry    Output
```

This loop continues until the evaluator accepts the result.

* * *

## Also Known As

**LLM as a Judge**

This is the more common industry term.

* * *

## Example

Generate code.

Evaluator checks:

-   Correctness
-   Security
-   Coding standards
-   Missing edge cases

If issues are found:

> "Regenerate with these improvements."

The process repeats until the output meets the required quality.

* * *

## Common Applications

-   Code generation
-   Writing assistants
-   Content moderation
-   Automated quality assurance
-   Test generation

* * *

# 6\. Agent Pattern

Unlike workflows, an agent has **no predefined execution path**.

Instead, it continuously:

1.  Reasons about the problem.
2.  Chooses actions.
3.  Uses tools.
4.  Observes results.
5.  Decides the next action.
6.  Repeats until the goal is achieved.

### Workflow

```
          User Goal
              │
              ▼
            LLM
              │
              ▼
        Select Tool
              │
              ▼
      Execute Action
              │
              ▼
     Observe Environment
              │
              ▼
        Goal Achieved?
         │          │
        No         Yes
         │          │
         └──────────┘
```

* * *

## Characteristics

-   Open-ended execution
-   Continuous reasoning
-   Dynamic decision making
-   Uses tools
-   Stops only after achieving its objective

This aligns with the modern definition of an AI agent:

> **An LLM with tools operating in a loop to achieve a goal.**

* * *

# Workflow vs Agent

| Feature | Workflow | Agent |
| --- | --- | --- |
| Execution path | Predefined | Dynamic |
| Planning | Mostly predetermined | Created during execution |
| LLM decision making | Limited to specific stages | Continuous |
| Predictability | High | Lower |
| Testing | Easier | More challenging |
| Typical use cases | Business processes, document pipelines | Coding assistants, browser automation, autonomous task execution |

* * *

# Combining Patterns

Real-world AI systems often combine several patterns.

Example:

```
User Request
      │
      ▼
Router
      │
      ▼
Prompt Chain
      │
      ▼
Orchestrator
      │
      ▼
Parallel Workers
      │
      ▼
Evaluator
      │
      ▼
Final Output
```

A production system may use routing, prompt chaining, parallelization, and evaluation together rather than relying on a single pattern.

* * *

# Key Takeaways

-   Anthropic introduced **five workflow patterns** and **one agent pattern** as common approaches to building agentic systems.
-   These patterns are **design ideas**, not mandatory architectures.
-   **Prompt Chaining** solves complex tasks through sequential LLM calls.
-   **Routing** directs requests to specialized prompts or workflows.
-   **Parallelization** executes independent tasks simultaneously.
-   **Orchestrator–Worker** uses LLMs to dynamically plan, distribute, and combine work.
-   **Evaluator–Optimizer (LLM as a Judge)** improves quality through iterative evaluation and refinement.
-   **Agents** differ from workflows by continuously reasoning and acting in a loop until a goal is achieved.
-   Production-grade AI systems frequently combine multiple patterns to balance flexibility, performance, and reliability.