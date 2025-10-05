# End-to-End Text Summarizer (Hugging Face, FastAPI, Docker, AWS CI/CD)

This repository implements a complete text summarization solution, from data ingestion and model fine-tuning to production deployment and continuous delivery.

## Key Features

- **Generative AI Fine-Tuning**  
    Fine-tuned a Pegasus summarization model on the SAMSum conversational dataset using Hugging Face Trainer API  
    Configured custom prompt templates and hyperparameters (warmup steps, gradient accumulation) to optimize summary coherence and length

- **Modular ML Pipelines**  
    Built reusable components for data ingestion, validation, transformation, training, and evaluation using a configuration-driven design  
    Managed experiment parameters via `config.yaml` and `params.yaml`, enabling reproducible training runs

- **Production-Grade API**  
    Developed a FastAPI application (`app.py`) with structured endpoints for summarization requests  
    Implemented robust logging, exception handling, and health checks for real-time monitoring

- **Containerization & Deployment**  
    Dockerized the application and model artifacts for consistent environments  
    Designed GitHub Actions workflows to build Docker images, push to AWS ECR, and deploy to EC2 as a self-hosted runner  
    Leveraged IAM roles with least-privilege policies for secure ECR and EC2 operations

## Repository Structure

```
.
config.yaml                 # Pipeline component configuration
params.yaml                 # Hyperparameters and paths
src/
    config/                 # Configuration manager
    components/             # Data, model, and evaluation modules
    pipelines/              # Orchestrated training & inference pipelines
    app.py                  # FastAPI application
    main.py                 # CLI entry point
requirements.txt            # Python dependencies
Dockerfile                  # Container build instructions
.github/
    workflows/              # CI/CD definitions (GitHub Actions)
README.md                   # Project documentation
```

## Getting Started

1. **Clone repository**  
   ```bash
   git clone https://github.com/From-Kishore-Kumar/End-to-End-Text-Summariser.git
   cd End-to-End-Text-Summariser
   ```

2. **Setup Conda environment**  
   ```bash
   conda create -n summary python=3.8 -y
   conda activate summary
   pip install -r requirements.txt
   ```

3. **Configure & Run**  
   - Update `config.yaml` and `params.yaml` with dataset paths and training settings  
   - Execute training & evaluation pipeline:  
     ```bash
     python main.py --stage train
     python main.py --stage evaluate
     ```  
   - Launch FastAPI server:  
     ```bash
     python app.py
     ```  
   - Access the summarization endpoint at `http://localhost:8000/summarize`

## CI/CD Deployment (GitHub Actions â†’ AWS)

1. **AWS Setup**  
   - Create IAM user with `AmazonEC2FullAccess` and `AmazonEC2ContainerRegistryFullAccess`  
   - Create ECR repository and note the URI  

2. **Configure GitHub Secrets**  
   ```text
   AWS_ACCESS_KEY_ID
   AWS_SECRET_ACCESS_KEY
   AWS_REGION
   AWS_ECR_LOGIN_URI
   ECR_REPOSITORY_NAME
   ```

3. **Self-Hosted Runner on EC2**  
   - Provision Ubuntu EC2 instance, install Docker, and register it as a GitHub Actions runner  
   - CI workflow builds Docker image, pushes to ECR, then deploys container on EC2 automatically  

---  
**End-to-end ML skills demonstrated:** generative AI fine-tuning, pipeline engineering, API development, containerization, and CI/CD for production deployments.
