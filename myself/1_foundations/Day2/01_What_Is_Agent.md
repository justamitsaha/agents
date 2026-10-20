# 1\. What is an AI Agent?

There is **no universally accepted definition** of an AI agent. However, the AI community has gradually converged on three increasingly precise definitions.

* * *

## Definition 1: AI that Works Independently

The earliest definition, popularized by OpenAI and Sam Altman, describes an AI agent as:

> **An AI system that can perform work independently on behalf of a user.**

### Characteristics

-   Given a high-level objective.
-   Executes tasks without constant human intervention.
-   Appears to "work on its own."

### Example

A user asks:

> "Find a restaurant with availability tonight."

The system:

1.  Opens a browser.
2.  Searches restaurant websites.
3.  Compares options.
4.  Makes decisions.
5.  Returns suitable results.

This behavior inspired the first understanding of AI agents.

* * *

# Definition 2: LLM Controls the Workflow

A more formal definition emerged in early 2025.

> **An AI agent is a system where an LLM controls the workflow.**

Instead of hardcoding every decision:

```
A → B → C
```

the application asks the LLM:

```
Which action should happen next?Options:- A- B- C
```

The LLM responds:

```
B
```

The application interprets the response and executes action **B**.

### Key Idea

The LLM is making decisions about the application's behavior.

Example:

```
Prompt
      │
      ▼
     LLM
      │
"Do Action B"
      │
      ▼
Application executes B
```

The LLM is therefore controlling the workflow.

* * *

# Important Mental Model

One of the most important concepts in AI engineering is understanding what an LLM actually does.

### An LLM only:

-   Receives tokens as input.
-   Predicts the most likely next tokens.
-   Returns generated text.

An LLM **does not**:

-   Execute code
-   Call APIs
-   Click buttons
-   Access databases
-   Use tools
-   Take actions

Those capabilities come from the surrounding application.

The application:

-   interprets the LLM output,
-   decides whether it represents an action,
-   executes code,
-   invokes tools,
-   manages state,
-   determines whether the task is complete.

Therefore:

```
LLM = Token Prediction Engine NOT Autonomous Software
```

This distinction is fundamental for building AI systems.

* * *

# Definition 3: LLM + Tools + Loop + Goal

The most widely accepted modern definition is:

> **An AI agent is an LLM with tools in a loop to achieve a goal.**

This definition combines four essential components.

## 1\. LLM

Provides reasoning and decision making.

* * *

## 2\. Tools

The LLM can invoke external capabilities such as:

-   Web search
-   APIs
-   Databases
-   File systems
-   Email
-   Google Sheets
-   Calculators
-   Code execution

Without tools, the LLM can only generate text.

* * *

## 3\. Loop

The system repeatedly:

1.  Thinks
2.  Chooses a tool
3.  Uses the tool
4.  Observes the result
5.  Thinks again

until the task is finished.

Example:

```
Goal

↓

Think

↓

Search Web

↓

Read Results

↓

Think Again

↓

Use Another Tool

↓

Repeat

↓

Goal Achieved
```

* * *

## 4\. Goal

The loop stops only when the objective has been completed.

* * *

# Formula

```
AI Agent

=

LLM
+
Tools
+
Loop
+
Goal
```

* * *

# Example

An investment assistant agent might:

1.  Read market prices.
2.  Read a Google Sheet portfolio.
3.  Calculate gains.
4.  Search recent news.
5.  Recommend portfolio changes.

This matches the modern definition because it:

-   uses an LLM,
-   accesses tools,
-   repeatedly reasons,
-   stops after completing the objective.

* * *

# LLM Call vs AI Agent

These two concepts should never be confused.

| LLM Call | AI Agent |
| --- | --- |
| Generates text | Completes tasks |
| Predicts tokens | Uses tools |
| Single inference | Multiple iterations |
| No memory of workflow | Maintains execution state |
| Cannot take actions | Executes actions through application code |

The intelligence comes from combining the LLM with orchestration logic.

* * *

# 2\. Agentic Design Patterns

A highly influential 2024 blog by Anthropic, **Building Effective Agents**, introduced two major categories of agentic systems.

Both are considered **agentic systems**:

1.  Workflows
2.  Agents

* * *

# Workflows

A workflow consists of:

-   Multiple LLM calls
-   Predefined execution paths
-   Controlled decision points

Example:

```
Start

↓

Clarify User Request

↓

Search Web

↓

Analyze Information

↓

Generate Report

↓

Finish
```

The LLM may make local decisions, but the overall structure is predetermined.

### Characteristics

-   Predictable
-   Repeatable
-   Easy to test
-   Fixed architecture
-   Limited execution paths

* * *

# Example: Deep Research

Deep research features in tools like ChatGPT typically follow a workflow:

1.  Ask clarifying questions.
2.  Search the web.
3.  Collect sources.
4.  Generate findings.
5.  Produce a final report.

Although LLMs are involved, the process follows a predefined sequence.

* * *

# Agents

Agents are more autonomous.

Instead of following fixed paths, they continually decide:

-   What should I do next?
-   Which tool should I use?
-   Have I completed the task?

Example:

```
Goal

↓

Reason

↓

Choose Tool

↓

Observe Result

↓

Reason Again

↓

Choose Next Action

↓

Repeat

↓

Goal Completed
```

There is no predetermined sequence.

### Characteristics

-   Dynamic
-   Open-ended
-   Flexible
-   Self-directed
-   Potentially many iterations

* * *

# Examples of Agents

Examples include:

-   GPT Agent (formerly Operator)
-   Claude Code
-   Codex
-   AI coding assistants
-   Autonomous browser agents

These systems continuously evaluate progress and decide their next actions until they determine the task is complete.

* * *

# Workflow vs Agent

| Feature | Workflow | Agent |
| --- | --- | --- |
| Execution path | Predefined | Dynamic |
| LLM decisions | Limited | Continuous |
| Predictability | High | Lower |
| Testing | Easier | More difficult |
| Flexibility | Moderate | High |
| Production suitability | Excellent | Depends on use case |

* * *

# Gray Area Between Them

Many real-world systems combine characteristics of both workflows and agents.

Examples:

-   Limited iterations (e.g., maximum of five reasoning cycles)
-   Mostly predefined flow with occasional autonomous decisions
-   Controlled use of tools within constraints

These hybrid systems balance flexibility with reliability.

* * *

# Why Production Systems Prefer Workflows

Commercial AI applications often favor workflows because they are:

-   Easier to validate
-   Easier to test
-   More predictable
-   More reliable
-   Better suited for regulated or business-critical environments

Even when LLMs make intermediate decisions, organizations typically constrain those decisions within a predefined workflow.

* * *

# Key Takeaways

-   There is no single universally accepted definition of an AI agent.
-   The modern consensus defines an AI agent as **an LLM with tools operating in a loop to achieve a goal**.
-   An LLM only predicts text; it does not inherently execute actions.
-   Application code interprets LLM outputs, invokes tools, manages execution, and determines task completion.
-   Anthropic distinguishes **workflows** (structured, predefined execution paths) from **agents** (dynamic, autonomous decision-making), though both are considered agentic systems.
-   Most production-grade AI systems favor workflows for their predictability, repeatability, and ease of testing, while fully autonomous agents are used where flexibility and open-ended reasoning are required.