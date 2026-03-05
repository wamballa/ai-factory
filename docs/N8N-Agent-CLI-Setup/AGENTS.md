# Documentation Agent Instructions

This directory contains documentation for the AI Factory infrastructure.

Primary file
setup.md

System architecture

Windows laptop
 ↓
VirtualBox
 ↓
Ubuntu VM
 ├ Codex CLI
 ├ Git
 ├ SSH server
 └ Docker
      └ n8n automation server
           ↓
        SSH execution
           ↓
        Codex agents

Responsibilities

Maintain and improve setup.md.

Rules

- Keep steps concise and numbered
- Ensure commands are correct for Ubuntu
- Use code blocks for terminal commands
- Do not remove working instructions unless replacing them with better ones
- Always read AGENTS.md, CONTEXT.md, and TODO.md before starting work.

## Shared Memory

The directory ../../memory contains shared information used by multiple agents.

Agents may read from these files but should modify them carefully.

## Shared Memory System

Agents collaborate through files in ../../memory.

inbox.md
    Messages between agents

tasks.md
    Shared task queue

ideas.md
    Discovered SaaS opportunities

decisions.md
    Important decisions

knowledge.md
    System knowledge

Rules

Agents may append to these files but should not delete historical information.

## Context Files

The file CONTEXT.md contains background information about the AI Factory system.

Always read CONTEXT.md before making documentation changes.

## Task Management

A file called TODO.md contains documentation tasks.

When working:

1. Read TODO.md
2. Select the highest priority unfinished task
3. Complete the task
4. Update documentation files
5. Move completed tasks to the Done section
