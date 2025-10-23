# Workflow CI - Heart Disease Prediction

MLflow Project with GitHub Actions CI/CD pipeline for automated model training.

## 🎯 Project Overview

This project implements **Kriteria 3: Membuat Workflow CI** with automated machine learning model training using MLflow Project and GitHub Actions.

**Level:** Advanced (4 pts) - MLflow Project + CI Workflow + Artifacts + Docker Images

## 🏗️ Project Structure

```
Workflow-CI/
├── .github/
│   └── workflows/
│       └── ci.yml                    # GitHub Actions workflow (Advanced)
├── .gitignore                        # Git ignore rules
├── MLProject/                        # MLflow Project folder
│   ├── modelling.py                 # Training script (from Membangun_model)
│   ├── conda.yaml                   # Environment config
│   ├── MLproject                    # MLflow Project config
│   ├── DockerHub.txt               # Docker Hub repository link
│   └── heart_preprocessing/         # Dataset
│       ├── X_train.csv
│       ├── X_test.csv
│       ├── y_train.csv
│       └── y_test.csv
├── artifacts/                        # Model artifacts (auto-generated)
│   ├── latest-model/                # Latest trained model
│   └── metadata.txt                 # Training metadata
└── README.md                         # This file
```

## 🚀 How It Works

### 1. MLflow Project Structure

- **MLproject**: Defines project configuration and entry points
- **conda.yaml**: Specifies conda environment and dependencies
- **modelling.py**: Main training script with MLflow tracking

### 2. GitHub Actions Workflow

Triggers on:
- Push to `main` branch
- Pull request to `main` branch
- Manual dispatch (workflow_dispatch)

Workflow steps:
1. Checkout code
2. Setup Python 3.12.7
3. Install Conda
4. Install MLflow and dependencies
5. Run MLflow Project (train model)
6. List MLflow artifacts
7. **Upload artifacts to GitHub Actions** (Skilled)
8. **Commit artifacts to repository** (Skilled)
9. **Build Docker image with `mlflow build-docker`** (Advanced)
10. **Login to Docker Hub** (Advanced)
11. **Push Docker image to Docker Hub** (Advanced)
12. Generate summary report

## 📝 Usage

### Local Testing

Test MLflow Project locally:

```bash
cd MLProject
mlflow run . \
  --env-manager=local \
  -P n_estimators=100 \
  -P max_depth=20 \
  -P min_samples_split=2 \
  -P random_state=42
```

### CI/CD Pipeline

1. **Push to GitHub:**
   ```bash
   git add .
   git commit -m "trigger: CI pipeline"
   git push origin main
   ```

2. **Automatic Execution:**
   - GitHub Actions automatically triggers
   - Runs MLflow Project
   - Trains model with specified parameters
   - Logs metrics to MLflow

3. **Manual Trigger:**
   - Go to GitHub Actions tab
   - Select "MLflow CI/CD Pipeline"
   - Click "Run workflow"

## 🔧 Configuration

### Parameters (in MLproject)

```yaml
n_estimators: 100       # Number of trees in Random Forest
max_depth: 20           # Maximum depth of trees
min_samples_split: 2    # Minimum samples to split node
random_state: 42        # Random seed for reproducibility
```

### Dependencies (in conda.yaml)

- Python 3.12.7
- MLflow 2.19.0
- Scikit-learn 1.3.2
- Pandas 2.1.4
- NumPy 1.26.2

## 📊 Model Training

**Algorithm:** Random Forest Classifier

**Dataset:** Heart Disease (preprocessed)
- Training: 734 samples
- Testing: 184 samples
- Features: 16

**Logged Metrics:**
- Accuracy
- Precision (weighted)
- Recall (weighted)
- F1-Score (weighted)
- ROC-AUC

## ✅ Kriteria 3 - Advanced (4 pts)

| Requirement | Status |
|-------------|--------|
| Membuat folder MLProject | ✅ |
| File modelling.py (from Membangun_model) | ✅ |
| File conda.yaml | ✅ |
| File MLproject | ✅ |
| Dataset preprocessing | ✅ |
| GitHub Actions workflow | ✅ |
| **Upload artifacts to GitHub** (Skilled) | ✅ |
| **Commit artifacts to repository** (Skilled) | ✅ |
| **Build Docker image with mlflow** (Advanced) | ✅ |
| **Push to Docker Hub** (Advanced) | ✅ |
| Tautan Docker Hub | ✅ |

### Features by Level:

**Basic (2 pts):**
- ✅ MLflow Project folder
- ✅ GitHub Actions CI workflow
- ✅ Automatic model training on trigger

**Skilled (3 pts):**
- ✅ All Basic features
- ✅ Upload artifacts to GitHub Actions
- ✅ Commit artifacts to repository

**Advanced (4 pts):**
- ✅ All Skilled features
- ✅ Build Docker image using `mlflow models build-docker`
- ✅ Push Docker image to Docker Hub
- ✅ Docker Hub repository link

## 🔗 Links

- **GitHub Repository:** [Add your repo URL]
- **GitHub Actions:** [Add your actions URL]
- **Docker Hub:** https://hub.docker.com/r/ganangsetyohadii/heart-disease-mlflow

## 🐳 Docker Deployment

### Pull Docker Image

```bash
docker pull ganangsetyohadii/heart-disease-mlflow:latest
```

### Run Model Server

```bash
docker run -p 5000:8080 ganangsetyohadii/heart-disease-mlflow:latest
```

### Test Model Inference

```bash
curl -X POST http://localhost:5000/invocations \
  -H 'Content-Type: application/json' \
  -d '{"inputs": [[0.5, 1, 0.4, -0.3, 1, -0.2, 1, 0.4, 1, 0, 1, 0, 0, 0, 0, 1]]}'
```

## 🔐 Required GitHub Secrets

For Advanced level (Docker Hub push), add these secrets to your GitHub repository:

1. Go to: Repository Settings → Secrets and variables → Actions
2. Add new repository secrets:
   - `DOCKER_USERNAME`: Your Docker Hub username
   - `DOCKER_PASSWORD`: Your Docker Hub access token or password

## 👤 Author

**Ganang Setyo Hadi**
- GitHub: [@notsuperganang](https://github.com/notsuperganang)

## 📄 License

Part of MLOps course submission - Dicoding Indonesia

---

**Note:** This project demonstrates CI/CD automation for machine learning using MLflow Projects and GitHub Actions.
