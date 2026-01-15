# AWS Cloud Projects

This repo contains two hands-on AWS projects demonstrating **serverless workflows** and **resilient scalable architecture**.

---

## Project 1 — Serverless Reminder App (S3 + API GW + Lambda + Step Functions + SES)
A browser-based reminder app hosted on **S3**, calling an **API Gateway** endpoint that triggers **Lambda + Step Functions** to schedule and send **meeting reminder emails** via **SES**.

**Stages**
1. Configure SES  
2. Build email Lambda (send via SES)  
3. Build Step Functions state machine (core scheduler)  
4. Build API Gateway + supporting Lambda  
5. End-to-end integration/testing  

---

## Project 2 — Evolutionary Scaling (WordPress → Resilient AWS Architecture)
Start with a **single EC2 instance** running WordPress + DB, then evolve into a **scalable, resilient** architecture.

**Stages**
1. Manual WordPress on EC2  
2. Automate build with Launch Template  
3. Move DB to RDS + update LT  
4. Move WP filesystem to EFS + update LT  
5. Add ASG + ALB + fix `WPHOME`  

---


