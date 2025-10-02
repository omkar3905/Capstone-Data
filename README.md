# A Framework for Multi-Modal Data Aggregation and Bitemporal Analysis

Overview
This project provides a complete framework for integrating heterogeneous data sources into a unified Data Lakehouse architecture using Delta Lake Time Travel. It demonstrates how to ingest, transform, and version data from multi-cloud and multi-modal sources while ensuring auditability, reproducibility, and secure data lineage.

The solution leverages Azure-native services for orchestration, automation, security, and monitoring, alongside open Lakehouse capabilities in Databricks.

Objectives
Build an auditable data lineage framework with Delta Lake Time Travel.

Aggregate structured and unstructured data from multi-cloud (Google Drive, Azure Storage, Azure SQL DB) sources.

Implement the medallion architecture (Bronze, Silver, Gold) for scalable ETL.

Ensure point-in-time querying, rollback, and historical reproduction of reports.

Integrate event-driven pipelines using Azure Function Apps for notifications.

Deploy infrastructure consistently with Terraform + Azure CLI under governance by Microsoft Entra ID and Azure Key Vault.

Architecture
Components
Infrastructure as Code (IaC): Terraform

Automation & CLI: Azure CLI

Version Control: Git & GitHub

Data Orchestration & Ingestion: Azure Data Factory, Azure Function App

Data Sources: Google Drive, Azure Blob Storage, Azure SQL Database

Processing & Analytics: Azure Databricks, Delta Lake (Time Travel), SQL

Security & Governance: Microsoft Entra ID (AAD), Azure Key Vault

Monitoring: Azure Monitor

Visualization: Power BI

Data Flow
Multi-Source Ingestion

Use Azure Data Factory pipelines to ingest:

From Azure SQL Database: structured data.

From Google Drive: CSV/JSON files via custom connectors or Logic Apps.

From Azure Blob Storage: unstructured/semi-structured files.

Data lands in the Bronze layer of Delta Lake.

Transformation (Medallion Architecture)

Databricks notebooks transform raw Bronze data → Silver layer (clean, conformed schema).

Further transformations → Gold layer (aggregated, business-ready data).

Temporal Data Management (Delta Time Travel)

Maintain Silver and Gold tables as versioned Delta tables.

Support queries to:

Reproduce historical BI reports.

Compare differences between specific versions.

Roll back to a stable state after failed loads.

Event-Driven Notifications

After Gold table materialization, Azure Function App triggers notifications (Teams/Email).

Deployment & Security

Deploy with Terraform and Azure CLI for consistency.

Manage secrets with Key Vault and enforce role-based access with Entra ID.

Key Features
Multi-cloud ingestion (Google + Azure sources).

Delta Lake Time Travel for auditability and recovery.

Serverless event-driven pipelines with Azure Functions.

Automated IaC deployment with secure governance.

Medallion data architecture (Bronze, Silver, Gold).

Learning Outcomes
Architecting a unified multi-modal ingestion workflow.

Implementing advanced Delta Lake Time Travel queries for compliance and auditability.

Integrating cloud-native orchestration + serverless extensions into data pipelines.

Designing end-to-end auditable and reproducible data lineage.

Resources & Documentation
Delta Lake Time Travel Documentation

ADF: Copy Data from Google Drive

Azure Function Triggers for Blob Storage

Visualization
Power BI connects to Gold tables for business-ready reporting.

Historical versions can be reproduced for compliance/regulatory dashboards.

Repository Structure
text
├── /infrastructure
│   ├── main.tf              # Terraform scripts for infra provisioning
│   ├── variables.tf
│   └── outputs.tf
├── /notebooks
│   ├── bronze_ingestion.py  # Landing raw data
│   ├── silver_transform.py  # Cleaning/conforming data
│   ├── gold_aggregation.py  # Final tables with business rules
│   └── time_travel_demo.py  # Delta time travel queries
├── /adf_pipelines
│   └── multi_source_ingestion.json
├── /functions
│   └── notify_on_gold.py    # Azure Function for notifications
├── /docs
│   └── architecture.png     # Architecture diagram
└── README.md
Getting Started
Prerequisites
Azure Subscription with Databricks Workspace

Terraform installed

Azure CLI installed

Power BI Desktop (optional for visualization)

Steps
Clone this repository:

bash
git clone https://github.com/your-repo-link.git
cd your-repo-link
Provision infrastructure using Terraform + Azure CLI:

bash
terraform init
terraform apply
Deploy Data Factory pipelines and Azure Functions.

Run Databricks notebooks for Bronze → Silver → Gold transformations.

Test Delta Lake time travel queries:

sql
SELECT * FROM gold_table VERSION AS OF 5;
SELECT * FROM gold_table TIMESTAMP AS OF '2025-10-01T00:00:00Z';
