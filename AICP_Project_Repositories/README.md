# AICP Project Repositories

- [aicp-ecs-claim-processor](https://github.com/mullamd/aicp-ecs-claim-processor) — ECS task that handles S3 → Textract → Glue → JSON processing
- [aicp-textract-callback-handler](https://github.com/mullamd/aicp_textract_callback_handler) — Lambda for Textract SNS → S3 (writes extracted/failed claim JSON)
- [aicp-claims-dq-job](https://github.com/mullamd/aicp-claims-dq-job) — Glue DQ: `claims-extracted-data/` → `DQ-validated-claims-data/` (pass) & `DQ-claims-failed-data/` (fail); validated records go to SageMaker
- [aicp-shap-sagemaker-container](https://github.com/mullamd/aicp-shap-sagemaker-container) — Custom SHAP-enabled container for SageMaker fraud detection
- [aicp-fraud-predictor-load-ecs](https://github.com/mullamd/aicp-fraud-predictor-load-ecs) — ECS microservice loading fraud predictions into Redshift
- [aicp-claims-api](https://github.com/mullamd/aicp-claims-api) — FastAPI service on ECS Fargate exposing claims & AI decisions
