# Agent Concepts and MCP Basics

## Workflow vs. Agent: The Core Distinction

Anthropic's "Building Effective Agents" essay makes an important architectural distinction. A **workflow** is a system where an LLM and its tools are orchestrated through predefined code paths — a human decides the sequence of steps in advance, and the LLM executes its part within that fixed structure. An **agent**, by contrast, is a system where the LLM dynamically directs its own process, deciding what to do next based on feedback from its environment (like the result of a tool call), rather than following a script someone else wrote.

The practical difference comes down to who owns the control flow. In a workflow, I own it — I decide step 1 happens before step 2, and the LLM has no say in that order. In an agent, the LLM owns it — it can look at what just happened and decide the next action itself, potentially taking a different path each time depending on what it finds.

## Classifying My FL-04 Pipeline

My "Ship an Automation Workflow v2" pipeline (source-grounded study notes via NotebookLM) is a **workflow, not an agent**. Three reasons:

1. **The steps were fixed in advance.** I designed a specific sequence — gather sources, generate a Study Guide, generate a Quiz, manually review — before I ever ran it. NotebookLM didn't decide this order; I did.
2. **Each step was manually triggered.** I clicked "Study Guide," waited for it, then separately clicked "Quiz." The tool never decided on its own to move to the next step or to skip a step based on what it found in the previous one.
3. **No environment feedback loop.** An agent would, for example, look at the sources it gathered, judge whether they were sufficient, and decide whether to search for more before moving on. My pipeline has no such judgment step — it runs the same fixed path every time regardless of what the sources actually contain.

This isn't a weakness. Anthropic's own guidance is to start with the simplest solution and only add agent-level complexity when the task actually needs flexible, model-driven decision-making. My pipeline is a well-defined, repeatable task (turn sources into study material) — exactly the kind of job a workflow is supposed to do well, predictably, every time.

## What MCP Is

The Model Context Protocol (MCP) is an open standard, described as a "USB-C port for AI applications," that lets an LLM connect to external tools and data sources through one consistent interface instead of a custom integration for every service. It defines three primitives:

- **Tools** — actions the model can take (e.g., search a file, read a document)
- **Resources** — data the model can access
- **Prompts** — reusable instruction templates

Without MCP, an LLM only knows what's in its training data and whatever text is typed into the chat. MCP is what lets it reach outside that boundary into a live, real system.

## What I Actually Did

I connected the Google Drive MCP connector to Claude and ran three tasks that a plain chat could never do:

1. **Listed my real, current Google Drive files** — Claude returned five actual files from my Drive (including a database lab file and an Excel spreadsheet), with real file IDs, sizes, and timestamps. A plain chat has no concept of "my Drive" at all; this only works because the connector gives Claude a live tool to call.
2. **Searched my Drive by keyword** — I asked it to find files with "Claude" in the title, and it returned the exact matching file, using Google Drive's real search syntax under the hood.
3. **Read the actual content of a specific file** by its file ID, rather than a general description — the connector fetched real content from a document that exists only in my personal cloud storage, not anywhere in Claude's training data.

## What My FL-04 Pipeline Would Need to Become an Agent

Right now the pipeline is a strict A→B→C sequence I trigger by hand. To become an agent, it would need the model to make a judgment call at each step rather than just executing it — for example, after gathering sources, the system itself would need to evaluate whether the source set is strong enough (are they using two-line snippets or comprehensive docs?) and decide, on its own, whether to search for more sources before generating the study guide, rather than always proceeding straight to the next fixed step regardless of source quality.
