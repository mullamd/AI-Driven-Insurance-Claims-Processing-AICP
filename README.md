# 🚀 AI-Driven Insurance Claims Processing (AICP)

End-to-end AWS-native pipeline for automated insurance claims:  
Textract → Glue Data Quality → SageMaker (XGBoost + SHAP) → ECS APIs → Redshift → QuickSight.  
CI/CD via GitHub Actions to Amazon ECR & ECS.


## ℹ️ About
End-to-end AI-Driven Insurance Claims Processing (AICP) with Claim API + Chatbot, built on AWS:  
S3, Textract, Glue DQ, SageMaker, ECS Fargate, Redshift, QuickSight, Step Functions, Lambda, EventBridge, SNS, Lex, CloudWatch, GitHub Actions.


## 📌 AICP Project Roadmap
The AI-Driven Insurance Claims Processing (AICP) project is built as an end-to-end AWS-native pipeline.  
It combines document ingestion, data quality, fraud detection, APIs, chatbot, orchestration, reporting, and CI/CD — all fully integrated.


## 🔄 AICP Step-by-Step Workflow

### Step 1 – Claim Submission
- Claim PDF/image uploaded to: `s3://aicp-claims-data/raw/claim-documents/`  
- EventBridge rule: `aicp-claim-upload-trigger`  
- Lambda: `aicp-claim-processing-trigger` starts the pipeline.  

### Step 2 – Document Processing
- ECS Fargate task: `aicp-ecs-claim-processor`  
- Calls Amazon Textract to extract structured claim data (policy number, claimant details, damage description).  
- Results saved to: `s3://aicp-claims-data/processed/claims-extracted-data/`

### Step 3 – Callback Handling
- Textract → SNS notification  
- Lambda: `aicp-textract-callback-handler` parses, cleans, and prepares extracted data.

### Step 4 – Data Quality Check
- Glue job: `aicp-claims-dq-job`  
  - ❌ **Fail:** record → `s3://aicp-claims-data/processed/claims-failed-data/` (SNS alert sent)  
  - ✅ **Pass:** record → `s3://aicp-claims-data/processed/DQ-validated-claims-data/`

### Step 5 – AI Fraud Detection
- Validated claims sent to SageMaker endpoint: `aicp-shap-sagemaker-container`  
- XGBoost + SHAP model outputs:  
  - Auto-Approve  
  - Manual Review  
  - Suspicious  
- Predictions saved to: `s3://aicp-claims-data/processed/fraud-predicted-claims-data/`

### Step 6 – Redshift Loading
- ECS Fargate task: `aicp-fraud-predictor-load-ecs`  
- Loads into Redshift schema `aicp_insurance`:  
  - `claims_processed`  
  - `claims_dq_status`

### Step 7 – Reporting & Insights
- QuickSight dashboards connect directly to Redshift.  
- Provides insights into:  
  - Claim volumes  
  - Fraud detection performance  
  - Data quality metrics  

## ⚙️ Orchestration & Notifications
- **AWS Step Functions** → orchestrates Textract → DQ → Fraud Scoring → Redshift  
- **AWS Lambda** → lightweight transformations  
- **Amazon EventBridge** → triggers on new claims  
- **Amazon SNS** → sends pass/fail and fraud alerts  


## 📊 Reporting & Monitoring
- QuickSight dashboards → claim volumes, fraud detection rates, data quality insights  
- CloudWatch → logs, metrics, alerts (ECS, Glue, Lambda)  

## 🔄 CI/CD & Automation
- GitHub Actions pipeline → builds Docker images → pushes to Amazon ECR → deploys to ECS Fargate  
- Enables rapid updates to Claim API & Fraud Predictor microservices  

## ✅ Project Highlights
- Claim intake → OCR → DQ → Fraud AI → Decision in minutes  
- Fraud detection with explainable AI (SHAP)  
- Integrated Claim API + Chatbot  
- Scalable, AWS-native, production-ready design  

**Designed & Implemented by: Mulla (AWS Cloud Data Engineer)**
