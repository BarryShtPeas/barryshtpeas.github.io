---
title: "Part 2: Azure Arc Setup: Pre-Requisites and Planning Gotchas"
description: "Get Azure Arc right from the start: key tips on connectivity, identity, OS setup, and common planning pitfalls before onboarding your resources."
date: 2025-06-05T10:30:57.028Z
draft: true
tags:
  - Azure
  - Azure Arc
  - Hybrid Cloud
  - Cloud Management
  - Governance
categories:
  - Cloud Architecture
  - Azure Arc
series:
  - Azure Arc Deep Dive
author: "author: James Lillystone"
toc: true
images:
  - ARC.png
cover:
  image: ARC.png
  alt: Azure Arc Overview
  caption: Azure Arc
  relative: true
---


## Overview

Getting started with Azure Arc is deceptively easy — but getting it right takes forethought. This post breaks down essential pre-requisites and the most common traps that derail successful deployments.

## 1. Network and Connectivity Requirements

Azure Arc requires outbound HTTPS access on port 443 to several Azure endpoints. In restricted environments, this can be a blocker.

- ✅ **Tip:** Allowlist required FQDNs rather than IPs to stay future-proof.
- ❗ **Gotcha:** Using a transparent proxy without SSL inspection may break onboarding.

[🔗 Microsoft Docs: Required URLs for Arc](https://learn.microsoft.com/en-us/azure/azure-arc/servers/network-requirements)

## 2. Identity and Access Management

You’ll need to register the `Microsoft.HybridCompute` and `Microsoft.GuestConfiguration` providers and assign roles correctly.

- ✅ **Best Practice:** Use a dedicated Service Principal for onboarding at scale.
- ❗ **Gotcha:** RBAC misconfiguration is a top reason onboarding fails silently.

## 3. OS and Agent Requirements

- Supported OS: Windows Server 2012 R2+, Ubuntu 16.04+, CentOS/RHEL 7+, etc.
- Ensure `Connected Machine Agent` has local admin privileges to install properly.

- ✅ **Best Practice:** Bake the agent into base images for auto-onboarded VMs.
- ❗ **Gotcha:** Server core installations often need additional tweaks or dependencies.

## 4. Tagging and Naming Standards

Set naming conventions and tags from the start — Arc doesn’t retro-tag easily.

- Example naming format: `arc-[hostname]-[location]-[env]`
- Use policy to enforce tags on connected machines

## 5. Region Selection and Resource Organization

- Azure Arc resources are metadata-only — but they're tied to a region for management.
- Use a dedicated RG per site or environment to simplify governance.

## 6. Gotchas Summary

| Area              | Pitfall                            | Solution                          |
|-------------------|-------------------------------------|-----------------------------------|
| Networking        | Blocked domains                     | Allowlist required URLs           |
| Identity          | Missing role assignments            | Use scoped Service Principals     |
| OS Support        | Agent fails on unsupported systems  | Check OS compatibility first      |
| Governance        | Inconsistent tags/names             | Apply policies early              |

## Up Next

In the next post, we’ll explore how to **onboard resources to Azure Arc at scale**, including PowerShell automation, DSC integrations, and template deployments.

---

*Need help setting up Azure Arc for your environment? Reach out or connect with me on [LinkedIn](https://www.linkedin.com/in/YOUR-HANDLE) or [GitHub](https://github.com/BarryShtPeas).*