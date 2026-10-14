---
title: "A2A use cases"
description: "Documented patterns for using an agent-to-agent protocol."
updated: "Wed Oct 14 2026 07:00:00 GMT+0700 (Indochina Time)"
url: "https://a2a.so/use-cases"
---

# A2A use cases

The examples below are patterns documented by public sources. They are not claims about named customer outcomes.

## Hosted A2A servers

Deploy an A2A server on AWS AgentCore Runtime, with OAuth or SigV4 authentication. [AWS documentation](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/runtime-a2a.md)

## Copilot Studio connections

Use a Copilot Studio agent to call external, third-party agents. [Microsoft announcement](https://www.microsoft.com/en-us/microsoft-cloud/blog/2025/05/07/empowering-multi-agent-apps-with-the-open-agent2agent-a2a-protocol/)

## Specialist delegation

An orchestrator can delegate to specialists built with different frameworks, such as a LangGraph orchestrator working with ADK or CrewAI agents. [Semantic Kernel example](https://devblogs.microsoft.com/semantic-kernel/guest-blog-building-multi-agent-solutions-with-semantic-kernel-and-a2a-protocol/)

## Commerce and payments

The Linux Foundation describes AP2 and A2A work as part of agentic commerce and payments. [Linux Foundation release](https://linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year)

## Test and inspect agents

Use [A2A Inspector](https://github.com/a2aproject/a2a-inspector) and the [A2A Technology Compatibility Kit](https://github.com/a2aproject/a2a-tck) for inspection and validation.

## Multi-agent samples

Public samples include a travel assistant and a slide-generation project that combine A2A with other agent tooling. [GitHub repository search](https://api.github.com/search/repositories?q=a2a+agent2agent+in:name,description,topics)

## Framework scaffolding

The AgentCore CLI documents A2A scaffolding with Strands, LangChain/LangGraph, and Google ADK. [AWS documentation](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/runtime-a2a.md)
