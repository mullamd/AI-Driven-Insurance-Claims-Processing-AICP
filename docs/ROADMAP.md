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

@"
# 🔄 AICP Step-by-Step Workflow

## Step 1 – Claim Submission
The process begins when a claim document — such as a PDF or image — is uploaded to the **Amazon S3 bucket**:  
`s3://aicp-claims-data/raw/claim-documents/`

- Upload triggers an **Amazon EventBridge** rule: `aicp-claim-upload-trigger`  
- This invokes a **Lambda function**: `aicp-claim-processing-trigger`  
- The Lambda kicks off the end-to-end workflow.

---

## Step 2 – Document Processing
- An **Amazon ECS Fargate task** (`aicp-ecs-claim-processor`) picks up the event.  
- It calls **Amazon Textract** to extract structured data (policy number, claimant details, damage description).  
- Extracted results are saved to:  
  `s3://aicp-claims-data/processed/claims-extracted-data/`

---

## Step 3 – Callback Handling
- Once Textract finishes, it sends a notification to an **Amazon SNS topic**.  
- That notification triggers a **Lambda function**: `aicp-textract-callback-handler`  
- The Lambda parses, cleans, and prepares the extracted data for validation.

---

## Step 4 – Data Quality Check
- The data flows into the **AWS Glue Data Quality job**: `aicp-claims-dq-job`.  

  - ❌ **Fail:** record is written to:  
    `s3://aicp-claims-data/processed/claims-failed-data/`  
    + SNS email alert sent.  

  - ✅ **Pass:** record is written to:  
    `s3://aicp-claims-data/processed/DQ-validated-claims-data/`  

---

## Step 5 – AI Fraud Detection
- Validated claims are sent to a **real-time Amazon SageMaker endpoint**, powered by:  
  `aicp-shap-sagemaker-container`  

- Inside, an **XGBoost model** with **SHAP explainability** scores each claim:  
  - Auto-Approve  
  - Manual Review  
  - Suspicious  

- Predictions saved to:  
  `s3://aicp-claims-data/processed/fraud-predicted-claims-data/`

---

## Step 6 – Redshift Loading
- An **ECS Fargate task** (`aicp-fraud-predictor-load-ecs`) loads fraud predictions into **Amazon Redshift**.  
- Data is stored in schema `aicp_insurance`, tables:  
  - `claims_processed`  
  - `claims_dq_status`

---

## Step 7 – Reporting & Insights
- **Amazon QuickSight** connects directly to Redshift.  
- Dashboards allow executives, analysts, and adjusters to monitor:  
  - Claim volumes  
  - Fraud detection performance  
  - Data quality metrics  

---
"@ | Out-File -Encoding utf8 docs\WORKFLOW.md


## ⚙️ Orchestration & Notifications
- **AWS Step Functions** orchestrate end-to-end claim flow (Textract → Glue DQ → Fraud Scoring → Redshift)  
- **AWS Lambda** executes lightweight tasks & transformations  
- **Amazon EventBridge** triggers pipeline execution when new claims arrive  
- **Amazon SNS** sends notifications for DQ pass/fail and fraud detection outcomes  

---

## 📊 Reporting & Monitoring
- **Amazon QuickSight** dashboards → Claim volumes, fraud detection rates, data quality insights  
- **Amazon CloudWatch** → Logs, metrics, and alerts for ECS tasks, Glue jobs, Lambda functions  

---

## 🔄 CI/CD & Automation
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
