---
title: "Part 3: Onboarding and Agent Deployment"
description: "Step-by-step onboarding for Azure Arc: servers, Kubernetes, and SQL. Covers automation options, tagging, and troubleshooting agent issues."
date: 2025-06-05T10:30:57.028Z
draft: false
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
![Image 1](ARC.png)

In Part 2 of this series, we looked at the planning steps critical to a successful Azure Arc deployment — including connectivity, identity, and OS support. Now it's time to roll up our sleeves and begin the onboarding process.

This post covers how to onboard various resource types into Azure Arc, including the tools and approaches available, and what to watch out for during setup.

---

## ⚙️ Resource Types and Onboarding Workflows

Azure Arc supports onboarding for several types of resources, each with its own process:

- **Arc-enabled Servers**: Physical or virtual machines (Windows/Linux)
- **Arc-enabled Kubernetes**: K8s clusters running anywhere (on-prem, EKS, GKE, etc.)
- **Arc-enabled SQL Server**: Installed SQL instances on Arc-enabled machines
- *(Arc-enabled Data Services and App Services are covered separately)*

Each resource is onboarded by installing an agent or integration component, which then registers it with Azure Resource Manager (ARM).

---

## 🚀 Onboarding Arc-enabled Servers

You can onboard servers using:

- **Azure Portal** (manual setup wizard)
- **Scripted approach** via the `azcmagent` CLI
- **ARM/Bicep templates** for repeatable deployments
- **Terraform** (via the Azure Arc provider)

Common steps:
1. Download and install the **Connected Machine Agent**
2. Register the machine with a **resource group and region**
3. Provide a **service principal or Azure Arc-enabled role** for identity
4. Confirm connection in the Azure portal

> ✅ Tip: Always tag resources as part of onboarding — retroactive tagging in hybrid environments can be messy.

---

## ☸️ Onboarding Kubernetes Clusters

Azure Arc-enabled Kubernetes lets you connect clusters **without changing** their existing control plane.

Options include:
- `az connectedk8s connect`
- Helm-based bootstrap
- Terraform with the Azure Provider
- Azure Arc Jumpstart scenarios (for scripted labs)

Key onboarding components:
- Cluster connect agent
- Optional GitOps agent (Flux)
- Azure Monitor for containers (if enabled)

> 💡 Arc connects to any CNCF-compliant cluster. You don’t need to run AKS to benefit.

---

## 🧠 Onboarding SQL Server (Arc-enabled)

Azure Arc can also project SQL Server instances into Azure for:
- Inventory and metadata
- Licensing visibility
- Integration with Defender for SQL

Pre-reqs:
- Azure Monitor agent installed
- SQL extension registered on the machine
- SQL assessment enabled

---

## 🛠️ Troubleshooting Onboarding

Here are some common gotchas:

- **Agent not connecting**? Check outbound ports and proxy configs.
- **Invalid credentials**? Ensure your service principal has `Azure Connected Machine Onboarding` role.
- **Kubernetes not appearing**? Validate Helm installation and namespace.
- **SQL not visible**? Verify monitoring agent and extension install status.

Use `azcmagent show` (for servers) or `az connectedk8s show` to confirm health.

---

## 🧪 Bonus: Automate Your Rollout

If you're onboarding hundreds of machines or clusters, use:

- **Azure Policy initiatives** with deployIfNotExists
- **Terraform modules** for server/k8s
- **Runbooks or scripts** with Azure Automation

Infrastructure as Code (IaC) is essential for consistency and traceability.

---

## ⏭️ Coming Up

In Part 4, we’ll explore **how to govern your Arc-connected resources at scale** using Azure Policy, Defender for Cloud, and Guest Configuration.

---