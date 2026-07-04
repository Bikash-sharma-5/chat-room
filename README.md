# 💬 ChatRoom Production-Ready CI/CD Pipeline (AWS EKS + ECR)

A fully automated, high-availability, production-grade deployment strategy and pipeline infrastructure blueprint for a containerized full-stack architecture. This system manages automated testing, artifact compilation, image optimization mapping, secure key injection, and Kubernetes orchestration utilizing **Amazon Elastic Container Registry (ECR)** and **Amazon Elastic Kubernetes Service (EKS)** configured with native **EKS Auto Mode** computes.

---

## 🏗️ Core Architecture Blueprint

The pipeline isolates workloads cleanly into logical boundaries, handling stateful runtime mutations securely away from edge networking zones.

```text
                                   [ DEPLOYMENT WORKFLOW LIFECYCLE ]

 [ Developer Local ] ──(Git Push)──► [ Jenkins Engine Core ]
                                        ├── Maven package (Spring Boot Core .jar)
                                        └── Node compilation (React static production bundle)
                                              │
                                              ├── (Secure Auth Handshake) ──► [ Amazon ECR Space ]
                                              │                                  ├── chat-backend:latest
                                              │                                  └── chat-frontend:latest
                                              ▼
                                   (Bypassed Validation Rollout)
                                              │
                                              ▼
                                 [ Amazon EKS Core (1.36) ]
                                              │
                    ┌─────────────────────────┴─────────────────────────┐
                    ▼                                                   ▼
         [ Public Edge Network ]                             [ Private Workload Slices ]
     AWS Elastic Load Balancer (ELB)                              Namespace: chat-app
            (Internet Edge Router)                                      ├── ConfigMaps & Opaque Secrets
                    │                                                   ├── 2x chat-frontend Pods (Nginx)
                    └───────────────(Proxied Traffic Route)────────────►└── 2x chat-backend Pods (Spring Boot)

