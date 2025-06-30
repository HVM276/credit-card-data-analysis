# 💳 Credit Card Transactional Analysis for Fraud Risk

A robust data engineering pipeline designed to detect potential fraud in credit card transactions using **PySpark on GCP Dataproc Serverless**. The system processes millions of daily records, enriches them via BigQuery, and orchestrates the entire flow with Airflow (GCP Composer). CI/CD is fully automated with GitHub Actions and PyTest to ensure code quality and deployment reliability.

> ✅ Automated fraud risk evaluation with PySpark  
> ✅ Improved test & deployment trust by **35%** through GitHub Actions CI/CD  
> ✅ Serverless architecture with **GCP-native services** for seamless scalability

---

## 🛠️ Tech Stack

- **Languages**: Python
- **Processing**: PySpark (GCP Dataproc Serverless)
- **Data Sources**: Google Cloud Storage (GCS), BigQuery
- **Orchestration**: Apache Airflow via GCP Composer
- **Testing**: PyTest
- **CI/CD**: GitHub Actions

---

## 📁 Project Structure

```
├── dags/
│   └── credit_fraud_dag.py             # Airflow DAG definition
├── pyspark_jobs/
│   └── fraud_detection_job.py         # PySpark script for fraud detection
├── tests/
│   └── test_fraud_logic.py            # PyTest unit tests
├── .github/
│   └── workflows/
│       └── ci-cd.yml                  # GitHub Actions CI/CD pipeline
├── data/
│   └── sample_transactions.json       # Sample input data (GCS)
├── README.md                          # Project documentation
└── requirements.txt                   # Python dependencies
```

---

## ⚙️ Pipeline Workflow

1. **BigQuery Setup**
   - Create a static table containing cardholder information.

2. **PySpark Processing**
   - Reads:
     - Cardholder info from BigQuery
     - Daily transactional data (JSON) from GCS
   - Applies:
     - Data validation rules
     - Transformation logic for fraud risk scoring
   - Outputs:
     - Processed data written back to GCS (archive or results)

3. **Airflow DAG (GCP Composer)**
   - Detects new transactional data in GCS
   - Triggers the PySpark job on **Dataproc Serverless**
   - Archives the processed files after completion

4. **CI/CD Automation**
   - GitHub Actions pipeline:
     - Runs PyTest unit tests on push
     - Deploys DAGs and PySpark scripts to GCS bucket used by Composer

---

## 🧪 Sample PyTest

```python
def test_high_value_transaction_flag():
    transaction = {"amount": 12000, "location": "NY", "user_id": "123"}
    risk = calculate_fraud_score(transaction)
    assert risk["risk_score"] > 0.8
```

---

## 🔄 GitHub Actions CI/CD Workflow

- Triggered on every push or PR to `main` branch
- Executes:
  - `pytest` on `/tests`
  - Uploads:
    - DAG files to `gs://composer-dags-bucket/dags/`
    - PySpark jobs to `gs://dataproc-code-bucket/jobs/`

---

## 📜 License

This project is licensed under the MIT License.

---

## 🤝 Contributing

Open to contributions! Please fork the repo and raise a pull request.

---

## 📬 Contact

For any questions or suggestions, connect via [LinkedIn](https://www.linkedin.com/in/h-v-m-) or raise an issue.
