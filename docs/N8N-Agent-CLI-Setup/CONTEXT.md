# AI Factory Context

This directory contains documentation for the AI Factory infrastructure.

The goal of the AI Factory is to create an automated pipeline that discovers,
researches, evaluates, and develops micro-SaaS opportunities.

## Infrastructure

Host machine
Windows laptop

Virtualization
Oracle VirtualBox

Virtual machine
Ubuntu Server

Core components

Codex CLI
Git
SSH server
Docker
n8n automation

## Architecture

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

## Documentation Files

setup.md
    Setup instructions for the AI Factory environment

AGENTS.md
    Instructions controlling how Codex behaves in this directory

../../TODO.md
    Root task board used by all agents

../../templates/project-template/
    Scaffold used for new micro-SaaS projects

## Purpose of Documentation Agent

Maintain and improve documentation for the AI Factory infrastructure.

Ensure setup instructions remain accurate and easy to follow.

## Shared Memory

The AI Factory uses a shared memory directory.

ai-factory/memory/

Files include:

ideas.md
knowledge.md
decisions.md

These files store long-term knowledge used by different agents.
