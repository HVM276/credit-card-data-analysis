# 🚀 Crypto Data Analysis - Near Real-Time Data Pipeline

This project demonstrates a near real-time Change Data Capture (CDC) pipeline using **DynamoDB Streams**, **Kinesis**, **Firehose**, **Lambda**, **Apache Hudi**, and the **AWS Glue ecosystem**. Designed to handle cryptocurrency transaction data, this pipeline enables continuous synchronization into S3 and facilitates upsert-ready analytics with Athena and QuickSight.

> ✅ Reduced crypto report lag by **50%**  
> ✅ Enabled versioned, upsert-ready datasets using **Apache Hudi**  
> ✅ Built low-latency dashboards on top of continuously updated data

---

## 🛠️ Tech Stack

- **Languages**: Python
- **Data Ingestion**: AWS DynamoDB, AWS Kinesis Data Streams, AWS Data Firehose
- **Processing & Transformation**: AWS Lambda, AWS Glue Jobs, Apache Hudi
- **Storage**: Amazon S3
- **Metadata & Cataloging**: AWS Glue Catalog, AWS Glue Crawler
- **Orchestration**: AWS Glue Triggers
- **Query & Visualization**: AWS Athena, AWS QuickSight

---

## 📁 Project Structure

```
├── lambda_transformer.py         # AWS Lambda function for processing Kinesis records
├── glue_hudi_job.py              # AWS Glue script for Apache Hudi upserts
├── application_properties.json   # Runtime config and metadata
├── setup_infra/                  # Scripts to set up DynamoDB, Kinesis, Firehose, and triggers
└── README.md                     # Project documentation
```

---

## ⚙️ Setup & Execution Steps

### 1. 🔧 DynamoDB + Kinesis Setup
- Create a DynamoDB table with `Streams` enabled.
- Configure a **Kinesis Data Stream** to capture DynamoDB Stream records.

### 2. 🔁 Firehose + Lambda Integration
- Set up an **AWS Kinesis Data Firehose** delivery stream targeting **S3**.
- Attach a **Lambda transformer** to Firehose (`lambda_transformer.py`) to filter, parse, or enrich CDC events.

### 3. ☁️ Glue Crawler & Table Creation
- Configure an **AWS Glue Crawler** to scan the Firehose S3 path and create a corresponding table in the **Glue Catalog**.

### 4. 🧠 Apache Hudi Upserts via Glue
- Create a **Glue Job** (`glue_hudi_job.py`) to process the S3 JSON data and perform **upserts** into **Hudi tables** on S3.

### 5. 🔄 Trigger Orchestration
- Create **Glue Triggers** to:
  - Run the **Crawler** every 15 minutes
  - Chain it to the **Glue Job** to ensure CDC data is consistently processed

### 6. 📊 Query & Visualize
- Query the Hudi tables via **Athena** using the AWS Glue Catalog schema.
- Connect the Athena datasets to **QuickSight** for crypto analytics dashboards.

---

## 🧪 Sample Athena Query

```sql
SELECT user_id, SUM(transaction_value) as total
FROM "crypto_db"."hudi_crypto_cdc"
WHERE currency = 'BTC'
GROUP BY user_id
ORDER BY total DESC
LIMIT 10;
```

---

## 📜 License

This project is licensed under the MIT License.

---

## 🤝 Contributing

Contributions are welcome! Please fork the repo, make your changes, and submit a PR.

---

## 📬 Contact

For questions or feedback, connect via [LinkedIn](https://www.linkedin.com/in/h-v-m-) or raise an issue.

