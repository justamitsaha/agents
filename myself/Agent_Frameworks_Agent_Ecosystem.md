# Agent Frameworks and the Agent Ecosystem


# Overview

This section introduces the broader **AI agent ecosystem**, explains what **agent frameworks** are, and discusses why they exist.

The lecture emphasizes an important point:

> **You do not need an agent framework to build an AI agent.**

Frameworks simply make development faster by abstracting repetitive tasks.

* * *

# 1\. The AI Agent Ecosystem

The AI agent landscape is still evolving rapidly and lacks standardized terminology.

The lecture categorizes the ecosystem into **four major types of offerings**:

1.  AI Builders
2.  Agent Products
3.  Agent Runtimes
4.  Agent Frameworks

* * *

# 1\. AI Builders

## Definition

AI Builders are visual or low-code platforms that allow users to create AI agents with minimal programming.

These platforms are designed for:

-   Developers
-   Business users
-   Low-code/no-code users

Typically using:

-   Drag-and-drop interfaces
-   Visual workflows
-   Pre-built integrations

* * *

## Examples

-   n8n
-   11Labs (voice-focused)
-   OpenAI Agent Builder
-   CrewAI Studio

* * *

## Purpose

Allow users to rapidly build agent workflows without writing extensive code.

* * *

# 2\. Agent Products

## Definition

Agent Products are finished applications that internally use AI agents to perform tasks.

Unlike builders, users interact with the product rather than creating agents themselves.

* * *

## Examples

-   Claude Code
-   Claude Work
-   OpenClaude
-   Claude Design

* * *

## Characteristics

These products:

-   Perform autonomous work
-   Execute multi-step tasks
-   Interact with tools
-   Hide implementation details from users

* * *

# 3\. Agent Runtimes

## Definition

Agent runtimes are environments where AI agents execute after deployment.

Think of them as the infrastructure responsible for running agent systems.

* * *

## Examples

General cloud runtimes:

-   AWS Lambda
-   Other cloud compute services

Specialized agent runtimes:

-   AWS Bedrock AgentCore
-   Claude Managed Agents
-   Vertex AI Agent Engine

* * *

## Responsibilities

A runtime provides:

-   Agent execution
-   Scaling
-   Communication
-   Deployment
-   Production hosting

* * *

# 4\. Agent Frameworks

## Definition

Agent frameworks are software libraries that help developers build AI agents.

Rather than being execution environments, they provide reusable code and abstractions for common agent functionality.

* * *

## Purpose

Reduce repetitive implementation effort.

Instead of manually implementing every component, developers can rely on framework utilities.

* * *

# Summary of the Ecosystem

| Category | Purpose | Primary Users | Examples |
| --- | --- | --- | --- |
| AI Builders | Visually build agents | Business users & developers | n8n, OpenAI Agent Builder, CrewAI Studio |
| Agent Products | Ready-to-use AI applications | End users | Claude Code, OpenClaude |
| Agent Runtimes | Execute deployed agents | Infrastructure teams | AWS Bedrock AgentCore, Vertex AI Agent Engine |
| Agent Frameworks | Build agent applications | AI engineers | OpenAI Agents SDK, CrewAI, LangGraph |

* * *

# 2\. What is an Agent Framework?

An agent framework is simply a collection of helper libraries that simplify building AI agents.

Instead of repeatedly writing boilerplate code, the framework provides reusable abstractions.

It is essentially an **abstraction layer** over common agent development tasks.

* * *

# 3\. Responsibilities of Agent Frameworks

Most frameworks simplify three major areas.

* * *

# A. Orchestration

Frameworks simplify chaining multiple LLM calls together.

Without a framework:

```
LLM 1

↓

LLM 2

↓

LLM 3
```

The developer manually:

-   manages prompts
-   passes outputs
-   handles errors
-   coordinates execution

With a framework, much of this orchestration is automated.

* * *

# B. Tool Calling

One of the most important framework features is **tool calling**.

Tool calling allows an LLM to access external capabilities.

Examples:

-   Search the web
-   Read a database
-   Access APIs
-   Retrieve stock prices
-   Execute Python
-   Send emails

Without a framework, implementing tool calling requires:

-   Prompt engineering
-   JSON formatting
-   Parsing responses
-   Manual execution logic

Frameworks automate much of this process.

* * *

# MCP Integration

Many frameworks also support **Model Context Protocol (MCP)**.

MCP enables developers to connect their LLM to tools created by other people.

Benefits include:

-   Reusable tools
-   Standardized integrations
-   Reduced development effort

* * *

# C. Structured Outputs

Normally, an LLM generates plain text.

Example:

```
The customer sentiment is positive.
```

Frameworks can instead return structured data.

Example:

```
CustomerAnalysis(
    sentiment="Positive",
    confidence=0.95
)
```

Internally, this is achieved by:

1.  Prompting the LLM to generate JSON.
2.  Parsing the JSON.
3.  Converting it into native programming objects.

Frameworks automate this conversion.

* * *

# 4\. Agent Loop Support

Frameworks also simplify building the core **agent loop**.

An agent repeatedly:

1.  Thinks
2.  Selects a tool
3.  Executes the tool
4.  Observes results
5.  Decides the next action

until the objective is completed.

```
Goal

↓

LLM

↓

Tool

↓

Observation

↓

Goal Complete?

↓

Repeat
```

This loop represents the modern definition of an AI agent:

> **An LLM with tools operating in a loop to achieve a goal.**

* * *

# 5\. Popular Agent Frameworks

The lecture introduces several frameworks, each with a different philosophy.

* * *

## OpenAI Agents SDK

Characteristics:

-   Lightweight
-   Flexible
-   Minimal abstraction
-   High developer control

Best suited for developers who prefer explicit control over implementation.

* * *

## Google ADK

Characteristics:

-   Lightweight
-   Similar philosophy to OpenAI Agents SDK
-   Simple development experience

* * *

## AWS Strands Agents

Characteristics:

-   Lightweight
-   Popular within AWS ecosystems
-   Integrates well with AWS services

* * *

# Opinionated Frameworks

Some frameworks prescribe a particular way of building agents.

These are called **opinionated frameworks**.

Advantages:

-   Faster development
-   Rich built-in functionality
-   Consistent architecture

Disadvantages:

-   Less flexibility
-   Harder to customize outside the intended design

* * *

## CrewAI

Characteristics:

-   Highly opinionated
-   "Batteries included"
-   Rich built-in capabilities
-   Rapid development

Because much functionality is provided out of the box, developers can build sophisticated systems quickly.

* * *

## LangGraph (with LangChain)

Characteristics:

-   Enterprise-focused
-   Structured workflows
-   Reliable execution
-   Strong support for production systems

Widely used where repeatability and robustness are important.

* * *

# Framework Comparison

| Framework | Style | Characteristics |
| --- | --- | --- |
| OpenAI Agents SDK | Lightweight | Flexible, minimal abstraction |
| Google ADK | Lightweight | Simple and developer-friendly |
| AWS Strands Agents | Lightweight | AWS ecosystem integration |
| CrewAI | Opinionated | Batteries included, rapid development |
| LangGraph | Opinionated | Enterprise-grade workflow orchestration |

* * *

# 6\. Do You Need a Framework?

The answer is:

> **No.**

Frameworks are conveniences, not requirements.

An AI agent can be implemented entirely with standard programming code.

Anthropic even recommends beginning without a framework to better understand how agent systems work internally.

* * *

# Benefits of Building Without a Framework

Writing an agent manually helps developers understand:

-   Orchestration
-   Tool calling
-   Agent loops
-   Prompt management
-   Output interpretation

Once these fundamentals are understood, frameworks become much easier to use effectively.

* * *

# Learning Strategy

The course intentionally starts without frameworks.

The progression is:

1.  Learn the underlying mechanics.
2.  Build an agent manually.
3.  Understand every component.
4.  Introduce frameworks to simplify development.

This ensures that developers understand **how** frameworks work rather than treating them as black boxes.

* * *

# 7\. Choosing an Agent Framework

There is no universally "best" framework.

The choice depends on:

-   Team expertise
-   Preferred programming style
-   Desired flexibility
-   Existing technology stack
-   Development speed requirements

Framework selection is generally less important than understanding the underlying concepts.

* * *

# Key Takeaways

-   The AI agent ecosystem consists of **AI Builders**, **Agent Products**, **Agent Runtimes**, and **Agent Frameworks**.
-   Agent frameworks are helper libraries that simplify building AI agents through reusable abstractions.
-   Most frameworks provide support for **orchestration**, **tool calling**, **structured outputs**, and **agent loops**.
-   **OpenAI Agents SDK**, **Google ADK**, and **AWS Strands Agents** are lightweight frameworks that offer greater flexibility and developer control.
-   **CrewAI** and **LangGraph** are opinionated frameworks that provide richer built-in functionality and faster development at the cost of reduced flexibility.
-   Building an agent does **not** require an agent framework; understanding the underlying mechanics first leads to a stronger foundation.
-   The best framework depends on the team's needs and preferences rather than a universally superior choice.