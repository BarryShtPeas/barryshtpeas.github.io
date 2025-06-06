---
title: "Part 5: Automation and GitOps with Azure Arc"
description: Automate Kubernetes config with GitOps via Azure Arc. Learn setup, Flux integration, and secure deployment of workloads at scale.
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

In this post, we explore one of the most powerful capabilities of Azure Arc-enabled Kubernetes: **GitOps automation**.

GitOps allows you to manage and deploy applications declaratively using a Git repository as the **single source of truth**. When combined with Azure Arc, it gives you full control over Kubernetes clusters running *anywhere* — including on-prem, in AWS, GCP, or edge sites.

---

## 🤖 What is GitOps?

GitOps is a model where:
- **Git repositories** store your desired cluster state (YAML manifests)
- An **agent** (usually Flux or Argo CD) continuously syncs the repo with the cluster
- Drift is automatically corrected
- All changes are traceable via Git history

With Arc-enabled Kubernetes, GitOps is built-in via **Flux v2**, integrated directly through the Azure portal or CLI.

---

## ⚙️ GitOps Architecture with Azure Arc

Once a cluster is connected with Arc, you can:
- Enable GitOps via the **Azure CLI** or **portal**
- Deploy one or more **Flux configurations**
- Point to a public or private Git repo
- Define sync intervals and scopes (cluster-wide or namespace)

Each config deploys Helm charts or raw YAML — perfect for:
- Baseline tools (e.g. Ingress controllers, monitoring agents)
- Workload deployments
- Custom policies or network rules

---

## 🚀 Setting Up GitOps with Azure Arc

Here’s a simple CLI example:

```bash
az k8s-configuration flux create \
  --cluster-name my-arc-cluster \
  --resource-group arc-rg \
  --cluster-type connectedClusters \
  --name baseline-deploy \
  --namespace flux-system \
  --url https://github.com/your-org/cluster-baseline \
  --branch main \
  --kustomization name=infra path=./manifests prune=true