---
title: "How I Passed AZ-104: Study Plan, Resources & Real-World Strategies"
subtitle: "From hands-on labs to smart timeboxing — everything I used to pass the Azure Administrator Associate exam"
summary: "AZ-104 is a gateway certification for becoming an Azure admin. In this post, I share my personal study plan, practical strategies, and go-to resources that helped me pass the AZ-104 exam with confidence."
date: 2025-08-16
draft: false
tags: ["AZ-104", "Azure Certification", "Cloud Engineer", "DevOps", "Azure Administrator"]
categories: ["Certifications", "Azure"]
cardimage: az-104.jpeg
featureimage: az-104.jpeg
caption: 
authors:
  - Mohammed: author.png
---

Preparing for the AZ-104 exam was a rewarding but challenging journey. As someone working in cloud and DevOps, I already had some Azure experience—but this exam required a **deeper operational understanding** across services. In this post, I’ll share the exact **study plan, resources, strategies, and tips** that helped me pass the exam and strengthen my day-to-day Azure skills.

---

## 🔍 Understanding What AZ-104 Covers

The AZ-104: Microsoft Azure Administrator Associate exam measures practical knowledge in:

1. **Azure identity and governance**
2. **Storage accounts and data management**
3. **Virtual machines and compute resources**
4. **Networking and connectivity**
5. **Monitoring, backup, and cost management**

It’s designed for those managing Azure in production, so **expect scenario-driven questions**, not just definitions.

---

## 🧠 My Study Strategy at a Glance

Here’s how I structured my preparation over 6–7 weeks:

- **Weekdays**: 1–2 hours of focused learning
- **Weekends**: Longer hands-on labs and recap sessions
- **Weekly focus**: One core skill area per week
- **Final week**: Practice exams + weak area reviews

I made sure to combine **Microsoft Learn**, **practice tests**, and **real Azure usage**—not just passive reading.

---

## 📅 My 6-Week Study Plan

### **Week 1: Azure Identity & Governance**

- RBAC, Azure AD, roles, subscriptions, policies
- **Tools Used**: Azure CLI + Microsoft Entra
- **Lab**: Created custom RBAC roles & enforced policies

📘 *Recommended Resource:*  
[Microsoft Learn: Manage identities and governance](https://learn.microsoft.com/en-us/training/paths/az-104-manage-identities-governance/)

---

### **Week 2: Storage**

- Blob vs File vs Table vs Queue
- Lifecycle rules, replication types (LRS, GRS)
- **Lab**: Used `az storage` CLI to automate blob upload/download

🔧 *Used Azure Storage Explorer & Microsoft Learn Modules*

---

### **Week 3: Virtual Machines & Compute**

- VMSS, availability sets/zones, extensions, custom script
- App Services and scaling plans
- **Lab**: Deployed VMs via portal and ARM templates

▶️ *Watched John Savill’s deep dives on VM internals*

---

### **Week 4: Networking**

- VNets, peering, NSGs, UDRs, VPNs, ExpressRoute basics
- Azure DNS, Load Balancer vs App Gateway
- **Lab**: Built a hub-and-spoke topology + peered VNets

🛠 *Tool:* Azure Network Watcher for testing and logs

---

### **Week 5: Monitoring & Backup**

- Log Analytics workspace, Azure Monitor, Alerts, Recovery Vaults
- Advisor recommendations and cost optimization

📊 *Lab:* Created alerts on VM CPU + dashboarded logs via KQL

---

### **Week 6–7: Revision & Practice Exams**

- Daily **practice tests (MeasureUp + TutorialDojo)**  
- Identified weak areas (e.g., NSG vs ASG, shared disks)
- Reread official docs for ambiguous areas

🎯 *Practice tip:* Timebox each practice test to simulate exam pressure

---

## 🧰 My Go-To Resources

Here are the exact tools and platforms I used:

| Resource | Type | Why I Used It |
|---|---|---|
| [Microsoft Learn](https://learn.microsoft.com/en-us/certifications/exams/az-104/) | Official | Free, interactive labs |
| [John Savill’s YouTube AZ-104 series](https://www.youtube.com/watch?v=V1Hk45XD6Qw&list=PLlVtbbG169nGlGPWs9xaLKT1KfwqREHbs) | Video | Expert deep dives, fast-paced |
| [TutorialDojo](https://tutorialsdojo.com/) / [MeasureUp](https://www.measureup.com/) | Practice exams | Accurate question patterns |
| [AZ-104 Study Materials](https://certs.msfthub.wiki/azure/az-104/) | Community | Study Materials |
| Azure Portal + CLI | Hands-on | Real practice beats theory |

---

## 🧠 Study Tips That Worked for Me

- **Timebox your sessions**: 45 mins study + 15 mins review beats hours of unfocused reading.
- **Always test what you learn**: Don’t just read about VNets—create one, peer it, break it.
- **Use the Azure free tier + sandbox** from Microsoft Learn.
- **Flag confusing practice questions** and revisit them weekly.
- **Join a community**: Reddit, Discord, and LinkedIn groups are helpful for clarifications.

---

## 📝 On the Exam Day

- You’ll have about **50–60 questions** in 120 minutes.
- Expect **drag-and-drop**, **case studies**, **CLI/PowerShell**, and **scenario questions**.
- Use the **“mark for review”** option liberally—skip and come back.

---

🔥 *Curveballs I got:*

- Shared Access Signatures (SAS) and Azure Files permissions
- **Fault domains vs update domains** — know how they apply in availability sets
- Service tiers for Blob storage (Hot, Cool, Archive)
- DNS resolution with private endpoints and custom DNS settings

---

## 🎉 Final Thoughts

Passing AZ-104 is very achievable, even if you're new to certifications. My biggest takeaway? **Don’t just aim to pass—aim to build real admin skills.** The exam will push you to become more confident in managing Azure in real-world environments.

Let me know if you’re preparing—I’m happy to share more templates, notes, or even jump on a study call. You've got this 💪

---

💬 **Got questions?**  
Reach out on [LinkedIn](https://www.linkedin.com/in/mohammedovich) or drop a comment.
