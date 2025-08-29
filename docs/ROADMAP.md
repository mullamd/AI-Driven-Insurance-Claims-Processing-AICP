# 🚀 AI-Driven Insurance Claims Processing (AICP)

End-to-end AWS-native pipeline for automated insurance claims:
Textract → Glue Data Quality → SageMaker (XGBoost + SHAP) → ECS APIs → Redshift → QuickSight.
CI/CD via GitHub Actions to Amazon ECR & ECS.

## ℹ️ About
End-to-end AI-Driven Insurance Claims Processing (AICP) with Claim API + Chatbot, built on AWS:  
S3, Textract, Glue DQ, SageMaker, ECS Fargate, Redshift, QuickSight, Step Functions, Lambda, EventBridge, SNS, Lex, CloudWatch, GitHub Actions.

@"
# 📌 AICP Project Roadmap

The **AI-Driven Insurance Claims Processing (AICP)** project is built as an end-to-end AWS-native pipeline.  
It combines **document ingestion, data quality, fraud detection, APIs, chatbot, orchestration, reporting, and CI/CD** — all fully integrated.

---

## 🚀 Phase 1: Claim Ingestion
- **Claim Submission** → PDFs/images via web portal or API uploaded to **Amazon S3**  
- **Document Processing** → **Amazon Textract (Async)** extracts claim details into structured JSON  
- **Data Validation** → **AWS Glue Data Quality** checks for completeness, accuracy, and duplicates  
- Valid data → S3 `processed/claims-extracted-data/`  
- Invalid data → S3 `processed/claims-failed-data/` with **SNS notifications**

---

## 🤖 Phase 2: AI Fraud Detection
- **Model Training** → **Amazon SageMaker (XGBoost + SHAP)** trained on historical claims data  
- **Explainability** → SHAP values for feature impact analysis  
- **Real-time Fraud Scoring** → Served via **SageMaker Endpoint** and ECS Fraud Predictor microservice  
- **Results Storage** → Fraud predictions appended into **Amazon Redshift** (`claims_processed` table)

---

## 🔗 Phase 3: APIs & Chatbot
- **AICP Claims API**  
  - Built with **FastAPI**  
  - Runs on **Amazon ECS Fargate**  
  - Endpoints:  
    - `GET /v1/claims/{claim_id}` → status + AI fraud explanation  
    - `GET /v1/claims/status/{claim_status}?days=&limit=` → list claims by status  

- **AICP ClaimBot**  
  - Built with **Amazon Lex**  
  - Integrated via **API Gateway + Lambda**  
  - Features:  
    - Check claim status  
    - Get AI explanation for fraud decisions  
    - Submit additional claim info  

---

## ⚙️ Phase 4: Orchestration & Notifications
- **AWS Step Functions** orchestrate end-to-end claim flow (Textract → Glue DQ → Fraud Scoring → Redshift)  
- **AWS Lambda** executes lightweight tasks & transformations  
- **Amazon EventBridge** triggers pipeline execution when new claims arrive  
- **Amazon SNS** sends notifications for DQ pass/fail and fraud detection outcomes  

---

## 📊 Phase 5: Reporting & Monitoring
- **Amazon QuickSight** dashboards → Claim volumes, fraud detection rates, data quality insights  
- **Amazon CloudWatch** → Logs, metrics, and alerts for ECS tasks, Glue jobs, Lambda functions  

---

## 🔄 Phase 6: CI/CD & Automation
- **GitHub Actions** pipeline → Builds Docker images → Pushes to **Amazon ECR** → Deploys to **ECS Fargate**  
- Enables rapid updates to Claim API and fraud predictor microservices  

---

## ✅ Project Highlights
- Claim intake → OCR → Data validation → Fraud detection → Decisions in minutes  
- Fraud detection with **explainable AI (SHAP)**  
- Integrated **Claim API** + **Chatbot** for transparency and customer interaction  
- Scalable, AWS-native, production-ready design  

---

**Designed & Implemented by: Mulla (AWS Cloud Data Engineer)**  
"@ | Out-File -Encoding utf8 docs\ROADMAP.md
