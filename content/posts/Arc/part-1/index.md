---
title: "Part 1: What is Azure Arc"
description: "Introduction to Azure Arc: what it is, why it matters, and how it extends Azure management to on-premises, multicloud, and edge environments."
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

Welcome to the first post in the Azure Arc Deep Dive series.

In today’s hybrid and multicloud world, organisations increasingly struggle to manage and secure resources across multiple environments and technology stacks. Whether it's virtual machines running on-premises, Kubernetes clusters in AWS, or databases at the edge, Azure tools have had limited reach — until now.

**Azure Arc** bridges this gap by extending Azure’s control plane to infrastructure hosted *anywhere*. It lets you project non-Azure resources into Azure Resource Manager (ARM), enabling unified management, governance, and security across environments.

---

## 🧩 What Exactly is Azure Arc?

Azure Arc is a portfolio of technologies designed to bring Azure’s management, policy, and security capabilities to:

- **Servers** (Windows/Linux, physical or virtual)
- **Kubernetes clusters** (including AKS on-prem, EKS, GKE)
- **SQL and PostgreSQL servers** (preview/built-in support)
- **Applications** via App Services and Logic Apps (Arc-enabled services)

Once onboarded, these resources behave like native Azure assets — you can assign RBAC, apply policy, monitor them in Azure Monitor, and even onboard them into Defender for Cloud.

---

## 🌍 Why Use Azure Arc?

Arc is particularly valuable when:

- You have **on-prem infrastructure** but want Azure governance
- You're in a **multi-cloud scenario** and need centralised control
- You manage **edge environments** like retail or manufacturing
- You're aligning with **compliance frameworks** and need consistent auditability
- You want to deploy and manage **Kubernetes at scale** using GitOps and policy

---

## 🏗️ How Arc Works (At a High Level)

At its core, Arc-enabled resources install an **agent** that registers them with Azure. This agent connects outbound over the internet and enables:

- Identity: the resource becomes an Azure object with its own ID
- Configuration: it can be tagged, grouped, and assigned policy
- Monitoring: you can collect logs and metrics centrally
- Security: Defender for Cloud assessments apply
- Automation: integrate with Update Management, Automanage, and GitOps

We'll go deeper into these capabilities throughout the series.

---

## 🚀 Coming Up

In the next post, we'll cover **what you need to do before onboarding resources** — including agent compatibility, connectivity planning, and identity setup. These early steps are often overlooked and can lead to frustrating failures or governance gaps later on.

---

*Need help setting up Azure Arc for your environment? Reach out or connect with me on [LinkedIn](https://www.linkedin.com/in/YOUR-HANDLE) or [GitHub](https://github.com/BarryShtPeas).*