# Risks, Best Practices, and Common Traps in Agentic AI

## Overview

While agentic AI enables powerful and flexible problem solving, it also introduces new challenges that traditional software systems do not face. This section discusses:

-   The risks of agentic AI
-   Techniques to mitigate those risks
-   Two common traps when designing AI agents
-   Best practices for building production-grade agentic systems

* * *

# 1\. Risks of Agentic AI

One of the greatest strengths of agentic AI is its ability to solve problems flexibly rather than following a rigid sequence of steps.

However, this flexibility also creates its biggest weakness:

> **Agentic AI is inherently unpredictable.**

* * *

## Sources of Unpredictability

Unlike deterministic software, agentic systems may produce different behaviors each time they execute.

### 1\. Execution Path

The agent may choose different sequences of actions to solve the same problem.

Example:

Run 1

```
Search → Read Database → Generate Report
```

Run 2

```
Search → Call API → Search Again → Generate Report
```

Both may reach the same goal through different paths.

* * *

### 2\. Output Variability

The same prompt can generate different responses across executions.

Example:

Question:

> "Summarize this document."

Different runs may produce different wording, emphasis, or structure while still being acceptable.

* * *

### 3\. Cost Variability

Because agents decide how many tools to use and how many reasoning iterations to perform:

-   Token usage varies
-   API calls vary
-   Execution time varies
-   Overall cost varies

Production systems must therefore account for variable operational costs.

* * *

# 2\. Mitigating Risks

There are two primary strategies for reducing these risks.

* * *

# A. Monitoring (Observability + Evaluation)

Monitoring provides visibility into how an agent behaves during development and production.

* * *

## Observability

Observability means collecting detailed execution traces so developers can understand what happened during every agent run.

Typical information includes:

-   LLM prompts
-   LLM responses
-   Tool calls
-   API invocations
-   Execution paths
-   Token usage
-   Latency
-   Cost
-   Errors

Without observability, debugging agentic systems becomes extremely difficult.

* * *

## Evaluations (Evals)

Monitoring should include systematic evaluation of the agent's effectiveness.

### Business-Level Evaluations

The most valuable evaluation measures whether the agent improves the business outcome it was built for.

Examples:

| Business Goal | Evaluation Metric |
| --- | --- |
| Sales assistant | Revenue generated |
| Lead generation | Number of qualified leads |
| Customer support | Resolution rate |
| Marketing | Conversion rate |
| Recruiting | Successful hires |

The ultimate question is:

> **Is the agent improving the business objective?**

* * *

### Technical Evaluations

Another type of evaluation measures the quality of the agent's outputs directly.

One common approach is:

-   Generate an answer.
-   Ask another LLM to evaluate it.
-   Accept or reject the output.

This corresponds to the **Evaluator–Optimizer** design pattern, commonly known as **LLM as a Judge**.

* * *

# B. Guardrails

Monitoring helps detect issues after they occur.

Guardrails help prevent issues before outputs are accepted.

OpenAI defines guardrails as mechanisms that ensure agents behave:

-   Safely
-   Consistently
-   Within intended boundaries

* * *

## What Are Guardrails?

Guardrails are application logic surrounding the LLM.

Instead of blindly trusting generated outputs, the application validates them before using them.

Examples include:

### Input Validation

-   Reject harmful prompts.
-   Validate required parameters.
-   Limit input length.

* * *

### Output Validation

-   Check JSON format.
-   Validate schema.
-   Prevent unsafe content.
-   Detect hallucinated values.
-   Ensure policy compliance.

* * *

### Workflow Constraints

Examples:

-   Maximum number of iterations
-   Maximum API budget
-   Timeout limits
-   Tool access restrictions

Guardrails make agent behavior more reliable and predictable.

* * *

# 3\. Common Trap #1 – Starting with the Solution Instead of the Problem

Many organizations approach AI projects by saying:

> "We need an AI agent."

This is the wrong starting point.

Instead, the first question should be:

> **What business problem are we trying to solve?**

* * *

## Solution-Oriented Thinking

Example request:

> "We need a strategy agent."

This describes a proposed solution, not the underlying business need.

* * *

## Problem-Oriented Thinking

Ask:

-   What issue exists?
-   Why is this important?
-   How will success be measured?

Example:

Initial request:

> "Build a culture agent."

After investigation, the real problem is:

-   Low employee morale
-   High employee attrition

Now the problem becomes measurable.

Possible metrics:

-   Employee retention
-   Satisfaction scores
-   Attrition rate

Only then can an AI solution be evaluated objectively.

* * *

# Why This Matters

**LLMs generate convincing text.**

They **do not** automatically solve business problems.

An agent may produce excellent-looking recommendations while having no measurable business impact.

Success must therefore be tied to measurable outcomes rather than believable outputs.

* * *

# 4\. Business Metrics Are Essential

Every agent should have a clearly defined success metric.

Examples include:

| Application | Success Metric |
| --- | --- |
| Sales assistant | Revenue generated |
| Customer support | Resolution rate |
| Writing assistant | Acceptance rate |
| Coding assistant | Successful deployments |
| Investment advisor | Portfolio performance |

Without measurable outcomes, it is impossible to determine whether an agent is successful.

* * *

# 5\. Common Trap #2 – Anthropomorphizing Agents

Anthropomorphism means treating AI systems as though they are human workers.

Example:

Designing an architecture with roles such as:

-   Market Research Agent
-   Trading Agent
-   Risk Manager Agent
-   Portfolio Manager Agent

Simply because those roles resemble human organizations.

* * *

## Why This Is a Mistake

LLMs are **not people** They are token generation engines.
They do not possess:

-   Intentions
-   Understanding
-   Human reasoning

They are statistical models that predict the most likely next tokens.

Design decisions should therefore be based on measurable performance rather than human organizational structures.

* * *

# 6\. Start Simple

The recommended development approach is:

1.  Build the simplest possible solution.
2.  Measure performance.
3.  Improve only when necessary.

Initial architecture:

```
User   │   ->Single Prompt   │   ->Single LLM   │   ->Output
```

Only introduce additional complexity if measurable improvements justify it.

Possible enhancements include:

-   Prompt chaining
-   Routing
-   Multiple agents
-   Evaluators
-   Orchestrators

Each addition should improve a business metric.

* * *

# 7\. Iterate Using Data

Architecture should evolve through experimentation.

The process is:

```
Build-> Measure -> Analyze -> Improve -> Measure Again
```

Avoid creating complex multi-agent architectures solely because they appear sophisticated.

* * *

# 8\. Believable Does Not Mean Correct

LLMs are optimized to generate text that sounds plausible.

They are **not** optimized to guarantee:

-   Truth
-   Accuracy
-   Business value

Therefore, AI engineers must validate whether generated outputs actually solve the intended problem.

* * *

# 9\. Handling Hallucinations

The lecture presents an important perspective on hallucinations.

From an AI user’s perspective:

> "The model hallucinated."

From an AI engineer’s perspective:

> **The system failed to handle expected model limitations.**

LLMs always produce statistically likely text.

It is the engineer's responsibility to:

-   Validate outputs.
-   Add guardrails.
-   Verify facts.
-   Build evaluation pipelines.
-   Detect and recover from errors.

Hallucinations should be treated as an **engineering challenge rather than an excuse.**

* * *

# 10\. Role of an AI Engineer

An AI engineer is responsible for transforming raw token predictions into reliable business outcomes.

Responsibilities include:

-   Designing workflows
-   Building guardrails
-   Monitoring execution
-   Evaluating quality
-   Managing tools
-   Measuring business impact
-   Improving system performance

The lecture summarizes this responsibility as:

> **Align next-token prediction with measurable business outcomes.**

* * *

# 11\. Meaning of "Agentic Engineer"

The term **Agentic Engineer** has become ambiguous.

It may refer to either:

### 1\. Engineer Using Agents

A software engineer who uses coding agents such as Claude Code or Codex to assist development.

* * *

### 2\. Engineer Building Agents

An AI engineer who designs, develops, and deploys agentic systems.

Because of this ambiguity, it is recommended to describe the role explicitly rather than relying on the term alone.

* * *

# Best Practices

When building agentic AI systems:

-   Start with a clearly defined business problem.
-   Define measurable success metrics before choosing an architecture.
-   Begin with the simplest possible solution.
-   Increase complexity only when data demonstrates improvement.
-   Monitor production systems using observability and evaluations.
-   Protect systems with guardrails.
-   Remember that LLMs generate plausible text—not guaranteed truth.
-   Treat hallucinations as engineering problems to be managed.
-   Evaluate success based on measurable business impact rather than convincing outputs.

* * *

# Key Takeaways

-   Agentic AI offers flexibility but introduces unpredictability in execution, outputs, and costs.
-   The primary strategies for managing these risks are **monitoring** (observability and evaluations) and **guardrails**.
-   Always begin with a **business problem**, not with the desire to build an AI agent.
-   Success should be measured using concrete business metrics, not by how convincing the generated content appears.
-   Avoid anthropomorphizing LLMs; they are statistical token predictors, not human decision-makers.
-   Build the simplest solution first, measure its effectiveness, and evolve the architecture only when it produces measurable improvements.
-   **Hallucinations are an engineering responsibility** to mitigate through validation, testing, and system design.
-   The core responsibility of an AI engineer is to convert probabilistic language generation into reliable, measurable business outcomes.