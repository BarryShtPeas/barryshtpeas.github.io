---
title: "Part 7: Lessons Learned and Gotchas"
description: "Hard lessons from real-world Azure Arc deployments: performance issues, monitoring limits, support boundaries, and billing surprises."
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



Welcome to the final part of the Azure Arc Deep Dive series. We've covered what Azure Arc is, how to plan and deploy it, and where it shines in real-world scenarios.

In this post, we’ll shift gears and share **lessons learned**, **common pitfalls**, and **"gotchas"** that you’re likely to encounter when deploying Arc in production.

---

## 🐌 Agent Performance and System Overhead

While lightweight in most cases, the **Connected Machine Agent** and **Kubernetes agents** can introduce:

- Memory and CPU overhead (especially on resource-constrained systems)
- Logging volume that can flood ingestion pipelines if not tuned
- DNS or proxy issues if outbound communication is filtered

> 💡 Tip: Use Log Analytics agent filtering and monitor resource usage after onboarding.

---

## 🧩 Monitoring and Visibility Limitations

Azure Arc gives you visibility — but **not parity** with native Azure resources:

- Update Management doesn’t support all OS types or edge scenarios
- Performance counters can be incomplete on certain Linux distros
- Guest Configuration may miss changes if not polled frequently

> 📝 Arc is powerful, but not a drop-in replacement for full Azure VMs.

---

## 🧱 Azure Policy & Guest Configuration Challenges

- `DeployIfNotExists` often fails silently if permissions or network rules are missing
- Guest Configuration requires **proper agent configuration**, which may break if the machine is imaged or renamed
- Policies can appear as “compliant” but not actually apply remediation

> 🔍 Always validate with a test resource group before assigning policies at scale.

---

## 🔒 Security Assumptions and Identity Pitfalls

- Machines onboarded with **interactive logins** may not persist identity across reboots or images
- Service principals must have very specific RBAC to enable consistent deployment
- If onboarding via automation, be careful not to expose credentials in pipeline logs or scripts

> ✅ Use Managed Identity and Key Vault integrations wherever possible.

---

## 💸 Unexpected Billing and Defender Costs

Azure Arc itself is free for basic use — **but**:

- Defender for Cloud plans **do charge** per node (server or cluster)
- GitOps sync, policy assignments, and Log Analytics **can trigger hidden costs**
- Data ingestion from edge/remote sites may be expensive if not throttled

> 📉 Use Cost Analysis and Azure Monitor filtering to stay within budget.

---

## 🧰 Operational Gaps in Large-Scale Environments

- Bulk onboarding at scale can hit throttling limits or identity conflicts
- Monitoring config drift across 100s of resources becomes hard without automation
- Arc status alerts aren’t always real-time — disconnected devices can appear healthy for hours

> 🔁 Combine Arc with Azure Lighthouse or custom alerts for enterprise-scale ops.

---

## 🧭 Final Thoughts

Azure Arc is an incredibly powerful tool — but it's not magic. Successful deployments depend on:

- Careful planning and connectivity validation
- Automation and IaC-first approaches
- Realistic expectations about parity and limitations

Used well, Arc can unify management across fragmented infrastructure and give you a clean control plane for even the messiest environments.

---

## 🙏 Thanks for Reading

This wraps up the **Azure Arc Deep Dive** series — I hope you’ve found it helpful. If you’ve used Arc in production, I’d love to hear your war stories, tips, or feedback.

You can connect with me on [LinkedIn](https://www.linkedin.com/) or contribute suggestions to the [GitHub repo](https://github.com/).

Stay secure — and good luck wrangling your hybrid cloud!