---
name: explain
description: Provide clear explanations of code, concepts, and system behavior with educational clarity. Use when the user wants to understand how code works, why a design exists, or how a system behaves.
---

# Explain

Provides clear explanations of code, concepts, and system behavior with educational clarity.

## Overview

Explain only after analysis. First understand the code, concept, or system, then tailor the explanation to the audience.

The goal is not to paraphrase code. The goal is to help the user understand:
- what it does
- why it exists
- how it behaves
- what trade-offs or risks matter

Good explanations are:
- **Accurate** — grounded in the actual code, docs, config, tests, or observable behavior
- **Layered** — simple first, then deeper detail
- **Structured** — organized in a logical sequence
- **Practical** — includes examples, edge cases, and implications when useful
- **Honest** — clearly distinguishes facts, inferences, and unknowns

## When to Use

Use this skill when the user asks you to:
- Explain a file, function, module, or code path
- Break down a concept, pattern, or framework usage
- Describe system behavior end to end
- Clarify architecture, control flow, or data flow
- Produce onboarding-style explanations for maintainers and collaborators
- Explain trade-offs, risks, or security implications of an implementation

**When NOT to use:**
- When the user wants implementation rather than explanation
- When you have not yet examined the relevant code or docs
- When the request is so broad that you first need to narrow the target

## Triggers

Common trigger phrases:
- "Explain this file"
- "Help me understand this code"
- "Walk me through this system"
- "Explain this at a basic/intermediate/advanced level"
- "Explain with examples"
- "Explain the security implications"

## Usage

This skill is primarily an analysis-and-explanation workflow.

Extract these from the user request when available:
- **Target:** file, symbol, concept, subsystem, or behavior
- **Level:** basic, intermediate, advanced
- **Format:** text, examples, walkthrough, Q&A
- **Context:** architecture, framework, product, security, performance

If the target, audience, or goal is unclear, ask one focused follow-up question before proceeding.

## Behavioral Flow

### 1. Analyze
Examine the relevant code, configuration, tests, and docs before explaining.

Inspect the relevant source material before explaining.

Typical sources include:
- code files
- configuration
- tests
- local documentation
- adjacent files needed to understand imports, call sites, interfaces, and runtime behavior

For code explanation, gather enough context to answer:
- What does it do?
- Why does it exist?
- How does data flow through it?
- What assumptions does it make?
- What external dependencies shape its behavior?
- What are the important edge cases or failure modes?

### 2. Assess
Determine the audience, explanation depth, and response format.

Perform assessment using signals from the request:
- **Audience clues:** beginner language, onboarding intent, senior-engineer terminology, urgency, or precision requested
- **Target complexity:** single function vs. subsystem vs. distributed behavior
- **User goal:** understand purpose, debug behavior, learn a concept, review architecture, or evaluate security implications
- **Requested output style:** summary, examples, walkthrough, comparison, or Q&A

If the user does not specify a level, infer it:
- **Basic** when the user asks for plain-English understanding, is clearly learning, or the topic is unfamiliar
- **Intermediate** by default for most engineering explanations
- **Advanced** when the user asks for internals, trade-offs, performance, failure modes, or architectural reasoning

If confidence is low, ask one follow-up question such as:
- "Do you want a high-level overview or an implementation-level walkthrough?"
- "Should I explain this like onboarding material or like a code review?"

### 3. Structure
Plan the explanation sequence with progressive complexity and logical flow.

A good default sequence is:
1. **What it is**
2. **Why it exists**
3. **How it works**
4. **Key components or steps**
5. **Example or walkthrough**
6. **Trade-offs, gotchas, or security notes**

For complex systems, break the explanation into subsystems rather than trying to explain everything at once.

### 4. Generate
Write the explanation with educational clarity.

Useful patterns:
- Start with a one-paragraph summary
- Use bullets for structure and sequence
- Reference specific files and symbols when discussing code
- Use short examples when they make behavior easier to understand
- Explain both the happy path and notable edge cases
- Call out uncertainty when the code or docs do not fully answer something

### 5. Validate
Before finishing, verify that the explanation is faithful to the source and useful for the audience.

Check:
- Did you actually read the relevant files?
- Are you describing what the code does now, not what you assume it should do?
- Did you distinguish between observed facts and interpretation?
- Did you answer the user’s likely why/how questions, not just restate code?
- Does the level match the user’s likely needs?

## Explanation Lenses

Apply these selectively based on the request and the code under discussion.

Choose lenses using simple heuristics:
- Use the **Educator Lens** when the user is learning, asks for a simple explanation, or needs progressive understanding
- Use the **Architect Lens** when the request is about structure, boundaries, system behavior, data flow, or design trade-offs
- Use the **Security Lens** when the code touches authentication, authorization, secrets, user input, trust boundaries, storage, networking, or anything safety-critical
- Combine lenses when appropriate, but do not force all three into every explanation

### Educator Lens
Optimize for learning:
- Define unfamiliar concepts
- Use progressive complexity
- Prefer concrete examples over abstract wording
- Anticipate likely confusion points

### Architect Lens
Optimize for system understanding:
- Explain module boundaries and responsibilities
- Show data flow and dependency flow
- Highlight trade-offs and design intent
- Connect local code to system-level behavior

### Security Lens
Optimize for risk awareness:
- Note trust boundaries and input validation
- Explain auth, authz, secrets handling, and error exposure where relevant
- Point out misuse risks, unsafe defaults, or attack surfaces
- Avoid revealing sensitive details unnecessarily

## Output Formats

Adapt the response to the user’s requested format.

### Text Summary
Best for quick understanding.

Structure:
- Summary
- How it works
- Important details
- Gotchas

### Example-Driven Explanation
Best for learning by demonstration.

Structure:
- Summary
- Small concrete example
- Step-by-step walkthrough of the example
- Variations or edge cases

### Interactive Walkthrough
Best for large or complex topics.

Structure:
- Short overview
- Break into sections
- End with a suggested next question or area to inspect

## Working Inside a Codebase

When explaining code in a repository:
- Examine the target file plus directly related files
- Look at call sites, types, tests, and config before making claims
- Reference file paths clearly
- Prefer statements like "In `src/auth/session.ts`, `createSession()`..." over vague summaries
- If behavior depends on runtime configuration, say so explicitly

For framework-specific requests:
- Read local project docs and relevant source files first
- If the project includes framework docs or examples in the repo, use them
- Do not claim official behavior unless it is supported by code or documentation you actually examined

## Response Template

Use this template when it fits:

```markdown
## Summary
[1-3 sentence overview]

## What it does
[Purpose and responsibility]

## How it works
1. [Step one]
2. [Step two]
3. [Step three]

## Key details
- [Important implementation detail]
- [Constraint, assumption, or dependency]
- [Edge case or failure mode]

## Example
[Small concrete example or scenario]

## Gotchas / Trade-offs
- [Non-obvious behavior]
- [Performance, maintainability, or security note]
```

## Anti-Patterns to Avoid

- Explaining before reading the relevant code or docs
- Restating syntax without explaining intent or behavior
- Being overly abstract when the user needs a concrete walkthrough
- Drowning a beginner in implementation detail
- Oversimplifying away important trade-offs for advanced requests
- Claiming certainty when parts of the behavior are inferred
- Ignoring security-sensitive implications in auth, data handling, or user input paths

## Red Flags

- You have not inspected the main file and at least one relevant adjacent context source
- The explanation contains no file or symbol references for code questions
- The explanation says what the code is "supposed" to do instead of what it does
- You skipped edge cases, assumptions, or failure modes in a complex flow
- You used jargon without defining it for a basic-level explanation

## Verification

Before completing an explanation, confirm:
- [ ] I examined the relevant code, docs, or configuration
- [ ] The explanation matches the observed implementation
- [ ] The depth matches the user’s level and intent
- [ ] The structure moves from simple to detailed
- [ ] Important assumptions, trade-offs, and edge cases are covered
- [ ] Any security-relevant concerns are called out when applicable
