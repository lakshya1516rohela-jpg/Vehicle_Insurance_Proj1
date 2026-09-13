
# 🚗 Vehicle MLOps — End-to-End Machine Learning Production Pipeline

<p align="center">

**An end-to-end, production-oriented MLOps system for building, training, evaluating, deploying, and serving machine learning models on AWS.**

<br/>

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![MLflow](https://img.shields.io/badge/MLOps-Model%20Lifecycle-orange)
![MongoDB](https://img.shields.io/badge/Database-MongoDB%20Atlas-green?logo=mongodb)
![AWS](https://img.shields.io/badge/Cloud-AWS-orange?logo=amazonaws)
![Docker](https://img.shields.io/badge/Container-Docker-blue?logo=docker)
![GitHub Actions](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-black?logo=githubactions)
![Linux](https://img.shields.io/badge/Server-Ubuntu-E95420?logo=ubuntu)

</p>

---

## 📌 Project Overview

This project demonstrates how a machine learning solution can be transformed from a **locally developed model into a deployable, cloud-hosted ML application** using MLOps principles.

Rather than treating machine learning as a single notebook-based workflow, this project separates the complete ML lifecycle into modular components:

```text
Data
  │
  ▼
Data Ingestion
  │
  ▼
Data Validation
  │
  ▼
Data Transformation
  │
  ▼
Model Training
  │
  ▼
Model Evaluation
  │
  ▼
Model Registry / S3
  │
  ▼
Prediction Pipeline
  │
  ▼
Docker Container
  │
  ▼
AWS EC2
  │
  ▼
Production Application
```

The project additionally implements **CI/CD automation using GitHub Actions**, a **self-hosted GitHub runner**, **Docker-based deployment**, **MongoDB Atlas for data storage**, and **AWS S3 for model storage**.

---

# 🎯 Why This Project?

A typical ML project often ends after:

> Train Model → Save Model → Show Accuracy

This project focuses on what happens **after the model works**.

It addresses practical production questions such as:

* How is data ingested from a remote database?
* How is data validated before entering the ML pipeline?
* How are transformations kept consistent?
* How is model training modularized?
* How do we determine whether a newly trained model is better?
* Where should trained models be stored?
* How can the application be containerized?
* How can deployment be automated?
* How can a trained model be served through an application?
* How can the entire workflow be reproduced on another machine?

---

# 🏗️ System Architecture

```text
                         ┌──────────────────────┐
                         │      User / Client   │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │  Prediction Pipeline │
                         │      / Web App       │
                         └──────────┬───────────┘
                                    │
                                    ▼
                    ┌──────────────────────────────┐
                    │       Trained ML Model       │
                    └──────────────┬───────────────┘
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │        AWS S3 Storage        │
                    │       Model Registry        │
                    └──────────────────────────────┘


        ┌──────────────────────────────────────────────────┐
        │                  TRAINING PIPELINE                │
        └──────────────────────────────────────────────────┘

                         MongoDB Atlas
                              │
                              ▼
                     ┌────────────────┐
                     │ Data Ingestion │
                     └───────┬────────┘
                             ▼
                     ┌────────────────┐
                     │ Data Validation│
                     └───────┬────────┘
                             ▼
                     ┌───────────────────┐
                     │ Data Transformation│
                     └────────┬──────────┘
                              ▼
                     ┌────────────────┐
                     │ Model Trainer  │
                     └───────┬────────┘
                             ▼
                     ┌────────────────┐
                     │Model Evaluation│
                     └───────┬────────┘
                             │
                    Better Model?
                       /          \
                     NO            YES
                     │              │
                     │              ▼
                     │       ┌──────────────┐
                     │       │ Model Pusher │
                     │       └──────┬───────┘
                     │              │
                     │              ▼
                     │       ┌──────────────┐
                     │       │    AWS S3    │
                     │       └──────────────┘
                     │
                     └──────────────► Keep Existing Model


                     CI/CD PIPELINE

      GitHub Repository
              │
              ▼
      GitHub Actions
              │
              ▼
      Self-Hosted Runner
              │
              ▼
          Docker Build
              │
              ▼
        Amazon ECR
              │
              ▼
          AWS EC2
              │
              ▼
       Running ML App
```

---

# ✨ Key Features

| Feature                      | Implementation                                  |
| ---------------------------- | ----------------------------------------------- |
| 🧩 Modular ML Pipeline       | Separate components for each ML lifecycle stage |
| 🗄️ Cloud Database           | MongoDB Atlas                                   |
| 🔍 Data Validation           | Schema-driven validation                        |
| ⚙️ Feature Engineering       | Dedicated transformation pipeline               |
| 🤖 Model Training            | Modular estimator architecture                  |
| 📊 Model Evaluation          | Performance-based model comparison              |
| ☁️ Model Storage             | Amazon S3                                       |
| 📦 Containerization          | Docker                                          |
| 🔄 CI/CD                     | GitHub Actions                                  |
| 🖥️ Self-Hosted Runner       | GitHub Actions → AWS EC2                        |
| ☁️ Cloud Deployment          | AWS EC2                                         |
| 🐳 Container Registry        | Amazon ECR                                      |
| 🔐 Environment Configuration | Environment variables / secrets                 |
| 📝 Logging                   | Centralized application logging                 |
| ⚠️ Exception Handling        | Custom exception framework                      |
| 🌐 Prediction API            | Application-based inference                     |
| 🧪 Training Endpoint         | `/training` route                               |
| 📁 Reproducible Structure    | Python package-based project architecture       |

---

# 🧰 Tech Stack

### Programming & ML

* **Python 3.10**
* Pandas
* NumPy
* Scikit-learn
* Jupyter Notebook

### MLOps & Engineering

* Modular Python package architecture
* Configuration management
* Logging
* Custom exception handling
* Data validation
* Feature engineering
* Model evaluation
* Model versioning / storage

### Database

* **MongoDB Atlas**
* PyMongo

### Cloud & Deployment

* **Amazon Web Services**
* Amazon S3
* Amazon ECR
* Amazon EC2
* AWS IAM

### DevOps

* **Docker**
* **GitHub Actions**
* Self-hosted GitHub Actions runner
* Linux / Ubuntu

### Application

* Flask
* HTML
* CSS
* Jinja templates

---

# 📂 Project Structure

```text
vehicle-mlops/
│
├── .github/
│   └── workflows/
│       └── aws.yaml
│
├── notebook/
│   ├── mongoDB_demo.ipynb
│   └── EDA_and_Feature_Engineering.ipynb
│
├── static/
│
├── template/
│
├── src/
│   │
│   ├── components/
│   │   ├── data_ingestion.py
│   │   ├── data_validation.py
│   │   ├── data_transformation.py
│   │   ├── model_trainer.py
│   │   ├── model_evaluation.py
│   │   └── model_pusher.py
│   │
│   ├── configuration/
│   │   ├── mongo_db_connection.py
│   │   └── aws_connection.py
│   │
│   ├── constants/
│   │   └── __init__.py
│   │
│   ├── data_access/
│   │   └── proj1_data.py
│   │
│   ├── entity/
│   │   ├── config_entity.py
│   │   ├── artifact_entity.py
│   │   ├── estimator.py
│   │   └── s3_estimator.py
│   │
│   └── utils/
│       ├── main_utils.py
│       ├── logger.py
│       └── exception.py
│
├── app.py
├── demo.py
├── template.py
├── requirements.txt
├── setup.py
├── pyproject.toml
├── config/
│   └── schema.yaml
├── Dockerfile
├── .dockerignore
├── .gitignore
└── README.md
```

---

# 🔄 ML Pipeline

## 1️⃣ Data Ingestion

The pipeline starts by retrieving raw data from **MongoDB Atlas**.

```text
MongoDB Atlas
      │
      ▼
MongoDB Connection
      │
      ▼
Fetch Records
      │
      ▼
Key-Value Data
      │
      ▼
Pandas DataFrame
      │
      ▼
Data Ingestion Artifact
```

The data-access layer abstracts database operations from the ML components, making the pipeline easier to maintain and test.

---

# 2️⃣ Data Validation

Before training, the incoming dataset is validated against a predefined schema.

The project uses:

```text
config/schema.yaml
```

to define expectations around the dataset.

The validation stage helps detect:

* Missing columns
* Unexpected columns
* Data type inconsistencies
* Schema mismatches
* Invalid dataset structure

This creates a clear boundary between **raw data** and **trusted ML data**.

---

# 3️⃣ Data Transformation

The transformation component prepares validated data for machine learning.

Typical responsibilities include:

```text
Validated Dataset
       │
       ▼
Feature Engineering
       │
       ▼
Data Transformation
       │
       ▼
Training Dataset
       │
       └──► Testing Dataset
```

The transformation logic is encapsulated within reusable components rather than being tied to a notebook.

---

# 4️⃣ Model Training

The model-training component is responsible for:

* Loading transformed datasets
* Training the ML estimator
* Generating predictions
* Saving the trained model
* Producing model artifacts

The estimator architecture keeps model-specific functionality separate from pipeline orchestration.

---

# 5️⃣ Model Evaluation

The project introduces a model-quality gate before deployment.

A newly trained model is not automatically promoted.

Instead:

```text
Existing Model
      │
      │
      ▼
Compare Performance
      ▲
      │
Newly Trained Model
      │
      ▼
Is improvement significant?
      │
   ┌──┴──┐
   │     │
  YES    NO
   │     │
   ▼     ▼
Push    Reject
Model   Model
```

The configured evaluation threshold is:

```python
MODEL_EVALUATION_CHANGED_THRESHOLD_SCORE = 0.02
```

This prevents blindly replacing a production model with a model that does not provide sufficient improvement.

---

# 6️⃣ Model Pusher

Models that successfully pass evaluation are pushed to **Amazon S3**.

Configured model storage:

```text
AWS S3
└── my-model-mlopsproj
    └── model-registry/
```

The S3 estimator abstraction provides functionality for:

* Uploading trained models
* Downloading models
* Managing model artifacts
* Integrating model storage with the ML pipeline

---

# ☁️ AWS Architecture

```text
                       AWS CLOUD
┌────────────────────────────────────────────────────┐
│                                                    │
│     ┌───────────────┐       ┌───────────────┐     │
│     │     ECR       │       │      S3       │     │
│     │               │       │               │     │
│     │ Docker Images │       │ ML Models     │     │
│     └───────┬───────┘       └───────────────┘     │
│             │                                      │
│             ▼                                      │
│     ┌─────────────────┐                            │
│     │      EC2        │                            │
│     │                 │                            │
│     │ Ubuntu Server   │                            │
│     │ Docker Runtime  │                            │
│     └────────┬────────┘                            │
│              │                                     │
│              ▼                                     │
│       Production App                              │
│                                                    │
└────────────────────────────────────────────────────┘
```

---

# 🐳 Dockerization

The complete application is packaged into a Docker image.

Benefits include:

* Consistent runtime environment
* Dependency isolation
* Reproducible deployments
* Easier cloud deployment
* Reduced "works on my machine" problems

Basic workflow:

```text
Source Code
    │
    ▼
Dockerfile
    │
    ▼
Docker Image
    │
    ▼
Amazon ECR
    │
    ▼
AWS EC2
    │
    ▼
Running Container
```

---

# 🔄 CI/CD Pipeline

One of the major goals of this project is to automate deployment.

```text
Developer
    │
    │ git push
    ▼
GitHub Repository
    │
    ▼
GitHub Actions
    │
    ▼
Self-Hosted Runner
    │
    ├── Build Docker Image
    │
    ├── Authenticate with AWS
    │
    ├── Push Image
    │
    ▼
Amazon ECR
    │
    ▼
AWS EC2
    │
    ▼
Deploy Application
```

A new commit can therefore trigger the deployment workflow without manually rebuilding and deploying the application.

---

# 🏃 Self-Hosted GitHub Runner

Instead of relying exclusively on GitHub-hosted infrastructure, this project configures an **AWS EC2 machine as a self-hosted GitHub Actions runner**.

```text
GitHub Actions
       │
       ▼
Self-Hosted Runner
       │
       ▼
AWS EC2
       │
       ├── Docker
       ├── Application
       └── Deployment
```

This provides greater control over the deployment environment and demonstrates practical CI/CD infrastructure management.

---

# 🐳 Amazon ECR

Amazon Elastic Container Registry is used as the private container registry.

Example repository:

```text
vehicleproj
```

Deployment flow:

```text
GitHub
   │
   ▼
Docker Build
   │
   ▼
ECR
   │
   ▼
EC2
   │
   ▼
Docker Container
```

---

# 🌐 Application Deployment

The application is hosted on an AWS EC2 Ubuntu server.

Once deployed, the application exposes the configured application port.

Example:

```text
http://<EC2-PUBLIC-IP>:5080
```

The application provides both:

### 🔮 Prediction

Users can interact with the deployed ML model through the prediction pipeline.

### 🏋️ Training

The project also exposes:

```text
/training
```

for triggering the model-training workflow.

---

# 🔐 Configuration & Secrets

Sensitive information such as:

* MongoDB connection strings
* AWS access keys
* AWS secret keys
* Cloud configuration

should **never be hardcoded into source code**.

Instead, the project uses environment variables and GitHub repository secrets.

Example:

```bash
export MONGODB_URL="mongodb+srv://..."
export AWS_ACCESS_KEY_ID="..."
export AWS_SECRET_ACCESS_KEY="..."
```

GitHub Actions secrets include:

```text
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_DEFAULT_REGION
ECR_REPO
```

> ⚠️ Never commit real credentials, `.env` files, AWS CSV credentials, or database passwords to GitHub.

---

# 📝 Logging & Exception Handling

Production ML systems need more than model code.

This project implements dedicated modules for:

### Logging

```text
src/utils/logger.py
```

provides structured application logging for debugging and monitoring execution.

### Exception Handling

```text
src/utils/exception.py
```

provides centralized custom exception handling so failures can be traced back to the responsible pipeline component.

Example pipeline visibility:

```text
Data Ingestion
      │
      ├── INFO: Connecting to MongoDB
      ├── INFO: Dataset fetched
      └── INFO: Artifact generated

Data Validation
      │
      ├── INFO: Schema validation started
      └── INFO: Validation successful
```

---

# 🧪 Exploratory Data Analysis

The project also includes notebooks for:

* Exploratory Data Analysis
* Understanding feature distributions
* Identifying data quality issues
* Feature engineering
* Understanding relationships between variables

However, the notebook is treated as an **exploration and experimentation environment**, while reusable production logic is moved into the `src/` package.

---

# 🧩 Modular Architecture

A key design principle is separation of responsibilities.

```text
components/
    │
    ├── Data Ingestion
    ├── Data Validation
    ├── Data Transformation
    ├── Model Trainer
    ├── Model Evaluation
    └── Model Pusher
```

Each component communicates through clearly defined **configuration and artifact entities**.

```text
ConfigEntity
     │
     ▼
Component
     │
     ▼
ArtifactEntity
     │
     ▼
Next Component
```

This makes the system easier to:

* Debug
* Test
* Extend
* Maintain
* Reuse
* Deploy

---

# 🛠️ Local Setup

## 1. Clone the Repository

```bash
git clone <your-repository-url>
cd <project-directory>
```

## 2. Create the Project Template

Run:

```bash
python template.py
```

This generates the initial project structure.

---

## 3. Configure the Python Package

The project uses:

```text
setup.py
pyproject.toml
```

to make local modules importable as a Python package.

For additional explanation, refer to:

```text
crashcourse.txt
```

---

## 4. Create the Virtual Environment

Using Conda:

```bash
conda create -n vehicle python=3.10 -y
conda activate vehicle
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Verify the environment:

```bash
pip list
```

---

# 🗄️ MongoDB Atlas Setup

Create a MongoDB Atlas project and configure a cluster.

Recommended development configuration:

```text
Provider: Default
Cluster: M0
Database User: <your-user>
```

Create a database user and configure network access.

> For production deployments, avoid unrestricted access such as `0.0.0.0/0` where possible. Restrict access to trusted IPs, networks, or private connectivity.

Retrieve the MongoDB connection string and store it securely as:

```text
MONGODB_URL
```

---

# ☁️ AWS Setup

The project uses AWS for:

```text
S3  → Model Storage
ECR → Docker Image Registry
EC2 → Application Hosting
IAM → Access Management
```

Recommended AWS region:

```text
us-east-1
```

Required credentials should be configured through environment variables or a secure secrets-management mechanism.

---

# 🚀 End-to-End Workflow

Once the infrastructure is configured, the complete lifecycle looks like:

```text
                 ┌──────────────┐
                 │ MongoDB Atlas│
                 └──────┬───────┘
                        │
                        ▼
                ┌───────────────┐
                │ Data Ingestion│
                └───────┬───────┘
                        ▼
                ┌───────────────┐
                │Data Validation│
                └───────┬───────┘
                        ▼
               ┌──────────────────┐
               │Data Transformation│
               └────────┬─────────┘
                        ▼
                ┌───────────────┐
                │ Model Training│
                └───────┬───────┘
                        ▼
                ┌────────────────┐
                │Model Evaluation│
                └───────┬────────┘
                        │
                  Better Model?
                    /       \
                  YES        NO
                   │          │
                   ▼          ▼
             ┌──────────┐   Reject
             │Model Push│
             └────┬─────┘
                  │
                  ▼
              ┌───────┐
              │ AWS S3│
              └───┬───┘
                  │
                  ▼
          Prediction Pipeline
                  │
                  ▼
             Docker Image
                  │
                  ▼
             Amazon ECR
                  │
                  ▼
              AWS EC2
                  │
                  ▼
           Production App
```

---

# 💡 Engineering Practices Demonstrated

This project demonstrates several practices relevant to production ML engineering:

### Software Engineering

* Modular architecture
* Reusable components
* Package-based imports
* Configuration management
* Custom exception handling
* Logging
* Separation of concerns

### Machine Learning

* EDA
* Feature engineering
* Data validation
* Model training
* Model evaluation
* Model promotion
* Prediction pipeline

### MLOps

* Reproducible pipelines
* Artifact management
* Model storage
* Model quality gates
* Automated deployment

### Cloud

* AWS IAM
* Amazon S3
* Amazon ECR
* Amazon EC2

### DevOps

* Docker
* GitHub Actions
* Self-hosted runners
* CI/CD automation
* Environment-based configuration

---

# 📈 What Makes This Project Different?

The main focus is not simply achieving a high model score.

The project demonstrates the transition:

```text
          Traditional ML
               │
               ▼
        Jupyter Notebook
               │
               ▼
          Train Model
               │
               ▼
         Save model.pkl
```

into:

```text
              MLOps
                │
                ▼
       Reproducible Pipeline
                │
       ┌────────┴────────┐
       ▼                 ▼
   Data Layer       ML Lifecycle
       │                 │
   MongoDB         Train → Evaluate
                       → Promote
                            │
                            ▼
                     Model Registry
                            │
                            ▼
                         Docker
                            │
                            ▼
                        CI/CD
                            │
                            ▼
                          AWS
                            │
                            ▼
                    Production App
```

The goal is to demonstrate **how ML systems can be engineered for repeatability, deployment, maintainability, and automation**.

---

# 🧑‍💻 Running the Project

After configuring MongoDB and AWS credentials:

```bash
python demo.py
```

For the application:

```bash
python app.py
```

The deployed application can then expose:

```text
Prediction → /
Training   → /training
```

---

# 🔮 Future Improvements

Potential extensions include:

* [ ] MLflow experiment tracking
* [ ] DVC-based dataset versioning
* [ ] Automated model monitoring
* [ ] Data drift detection
* [ ] Model drift detection
* [ ] Unit and integration testing
* [ ] Code quality checks with pre-commit
* [ ] Static analysis with Ruff
* [ ] Automated test execution in CI
* [ ] Infrastructure as Code using Terraform
* [ ] AWS CloudWatch monitoring
* [ ] HTTPS with a reverse proxy
* [ ] Kubernetes deployment
* [ ] Automated rollback strategy
* [ ] Model explainability using SHAP
* [ ] Production model metrics dashboard

---

# 📚 Learning Outcomes

By building this project, you gain hands-on experience with:

```text
Python
  ↓
Software Engineering
  ↓
Machine Learning
  ↓
MLOps
  ↓
Docker
  ↓
CI/CD
  ↓
AWS
  ↓
Production Deployment
```

This makes the project particularly useful as a portfolio demonstration for roles involving:

* Machine Learning Engineering
* MLOps Engineering
* Data Science
* AI Engineering
* Cloud Engineering
* Python Development

---

# 👨‍💻 Author

**Your Name**

Machine Learning | Data Science | MLOps | Cloud

⭐ If you found this project useful, consider giving the repository a star!

---

## ⭐ Project Summary

> **A complete MLOps implementation demonstrating how a machine learning model can move from raw data ingestion to automated cloud deployment using MongoDB, Python, AWS, Docker, GitHub Actions, and modular ML pipeline architecture.**

---

<p align="center">

### 🚀 From Data → Model → Container → Cloud → Production

</p>


