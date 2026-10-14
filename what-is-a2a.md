---
title: "What is A2A?"
description: "The basic objects and transports in the Agent2Agent protocol."
updated: "Wed Oct 14 2026 07:00:00 GMT+0700 (Indochina Time)"
url: "https://a2a.so/what-is-a2a"
---

# What is A2A?

The Agent2Agent (A2A) protocol gives independently built agents a shared way to discover capabilities, exchange messages, and manage work. [A2A documentation](https://a2a-protocol.org/)

## The core objects

An Agent Card is published at `/.well-known/agent-card.json`. It describes an agent's skills and interfaces so another agent can discover it. [AWS AgentCore A2A guide](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/runtime-a2a.md)

Tasks represent units of work. Messages carry Parts, including text, raw data, URLs, and media. [A2A v1.0 changes](https://a2a-protocol.org/latest/whats-new-v1/)

## Transports and v1.0

A2A supports JSON-RPC, gRPC, and REST transports. Version 1.0 added verb-style operations, a unified Part model, `supportedInterfaces`, signed Agent Cards, device-code OAuth, and cursor pagination. [A2A v1.0 changes](https://a2a-protocol.org/latest/whats-new-v1/)

## A2A and MCP

MCP is for an agent’s connection to tools and data; A2A is for agent discovery, delegation, and collaboration. They are complementary protocols. [AAIF ecosystem overview](https://aaif.io/blog/where-a2a-fits-in-the-open-agent-ecosystem)
