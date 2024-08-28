# Kubernetes for Data Engineering

This repository contains the necessary configuration of an e-commerce company seeking to build a scalable and automated data pipeline management system to process and analyze real-time data from multiple sources, including website interactions, order management systems, inventory databases, and customer feedback. The goal is to achieve efficient data ingestion, processing, and monitoring while maintaining flexibility in scaling and managing data engineering tasks.

## Objective 
Implement a Kubernetes-based data engineering environment with Apache Airflow for orchestrating complex workflows, enabling real-time data processing, scalability, and efficient resource management.

## Repository Structure

The repository is organized as follows:

```
.
├── dags
│   ├── fetch_and_preview.py
│   └── hello.py
└── k8s
    ├── dashboard-adminuser.yaml
    ├── dashboard-clusterrole.yaml
    ├── dashboard-secret.yaml
    ├── recommended-dashboard.yaml
    └── values.yaml
```

## Components

- Kubernetes Cluster: A scalable infrastructure layer that provides the foundation for deploying and managing containerized applications, such as Apache Airflow and other data engineering tools.
- Kubernetes Dashboard: A user-friendly web interface for monitoring and managing Kubernetes clusters, providing insights into resource utilization, application performance, and cluster health.
- Apache Airflow: DAGs (Directed Acyclic Graphs): Programmatically define, schedule, and monitor data engineering workflows. Use DAGs to manage tasks like data extraction, transformation, loading (ETL), and data quality checks.
- Helm: A package manager for Kubernetes that simplifies the deployment and management of applications on Kubernetes clusters, including Apache Airflow.

## Implementation
- Data Ingestion: Use Airflow DAGs, such as fetch_and_preview.py, to periodically fetch data from various sources, like transactional databases, REST APIs, or third-party analytics services.
These workflows are scheduled to run at specified intervals (e.g., hourly or daily) to ensure timely data ingestion.
- Data Processing and Transformation: Define and schedule additional DAGs in Apache Airflow to handle data transformation tasks, such as cleaning, normalization, aggregation, and joining disparate datasets.
Utilize Kubernetes' ability to scale resources dynamically to handle varying workloads, ensuring high performance and efficient processing.
- Monitoring and Management: Use the Kubernetes Dashboard to monitor the health and performance of the cluster, track resource usage, and identify any issues or bottlenecks in real-time. Airflow’s web UI enables detailed monitoring of workflow execution, failure detection, and alerting, ensuring data pipeline reliability and data quality.

### DAGs
- `fetch_and_preview.py`: A DAG for fetching data and providing a preview.
- `hello.py`: A simple example DAG to demonstrate basic Airflow concepts.

### Kubernetes (k8s) Configuration
- `dashboard-adminuser.yaml`: YAML file for setting up an admin user for the Kubernetes Dashboard.
- `dashboard-clusterrole.yaml`: YAML file defining the cluster role for the Kubernetes Dashboard.
- `dashboard-secret.yaml`: YAML file for managing secrets used by the Kubernetes Dashboard.
- `recommended-dashboard.yaml`: YAML file for deploying the recommended Kubernetes Dashboard setup.
- `values.yaml`: YAML file containing values for customizing the Kubernetes setup.

## Getting Started

### Prerequisites

- A Kubernetes cluster
- `kubectl` installed and configured
- Helm (optional, but recommended for managing Kubernetes applications)

### Setup

1. **Deploy the Kubernetes Dashboard:**

   To deploy the Kubernetes Dashboard, apply the YAML files in the `k8s` directory:

   ```bash
   kubectl apply -f k8s/
   ```

   This will set up the Kubernetes Dashboard with the necessary roles and permissions.

2. **Accessing the Kubernetes Dashboard:**

   To access the Dashboard, you may need to start a proxy server:

   ```bash
   kubectl proxy
   ```

   Then, access the Dashboard at: `http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/`.

   Use the token generated for the admin user to log in (see `dashboard-secret.yaml`).

3. **Deploy Apache Airflow:**

   You can deploy Apache Airflow using Helm or by applying custom YAML files. For Helm:

   ```bash
   helm repo add apache-airflow https://airflow.apache.org
   helm install airflow apache-airflow/airflow -f k8s/values.yaml
   ```

   This will deploy Airflow with the settings defined in `values.yaml`.

4. **Adding DAGs to Airflow:**

   Copy your DAG files (e.g., `fetch_and_preview.py`, `hello.py`) into the DAGs folder of your Airflow deployment. The method of copying depends on your Airflow setup (e.g., using Persistent Volume, Git-sync).

### Usage

- **Kubernetes Dashboard:** Use the Dashboard to monitor and manage the Kubernetes cluster.
- **Apache Airflow:** Access the Airflow web UI to manage, schedule, and monitor workflows.


