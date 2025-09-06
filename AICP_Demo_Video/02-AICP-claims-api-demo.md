# AICP Claims API Demo 🎥

This demo showcases the AICP Claims API — a FastAPI-based microservice running on AWS ECS Fargate, integrated with GitHub Actions CI/CD, Amazon ECR, and Amazon Redshift.  
It enables real-time querying of insurance claim data from the AICP system through REST endpoints, tested via Swagger UI and Postman.

🔗 **Watch on YouTube:**  
https://youtu.be/s_7DXZwPWFw

📂 Endpoints:
- `GET /v1/claims/{claim_id}` → Returns claim details + AI fraud detection fields
- `GET /v1/claims/status/{status}?days=&limit=` → Lists claims by status (Auto-Approve, Manual Review, Suspicious)
