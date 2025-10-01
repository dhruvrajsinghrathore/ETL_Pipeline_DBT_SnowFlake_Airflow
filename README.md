# ETL Pipeline with dbt, Snowflake, and Airflow

This project implements a complete ETL pipeline using:
- **dbt** for data transformation
- **Snowflake** as the data warehouse
- **Airflow** for orchestration

## Project Structure

```
ETL_pipeline_DBT_Snowflake_Airflow/
├── data_pipeline/          # dbt project
│   ├── models/
│   │   ├── staging/        # Staging models
│   │   └── marts/          # Mart models
│   ├── tests/              # dbt tests
│   ├── macros/             # dbt macros
│   ├── dbt_project.yml     # dbt configuration
│   └── packages.yml        # dbt packages
├── dbt_dag/                # Airflow DAGs
│   ├── dags/               # Airflow DAG files
│   ├── requirements.txt     # Python dependencies
│   └── Dockerfile          # Docker configuration
└── .gitignore              # Git ignore rules
```

## Setup Instructions

### Prerequisites
- Python 3.8+
- Docker
- Snowflake account
- Airflow

### 1. Setup dbt Project
```bash
cd data_pipeline
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install dbt-snowflake
dbt deps
```

### 2. Configure Snowflake Connection
Update `~/.dbt/profiles.yml` with your Snowflake credentials.

### 3. Run dbt Models
```bash
dbt run
dbt test
```

### 4. Setup Airflow
```bash
cd dbt_dag
astro dev start
```

## Features

- **Staging Models**: Raw data transformation
- **Mart Models**: Business-ready data marts
- **Data Tests**: Automated data quality checks
- **Airflow Orchestration**: Scheduled pipeline execution
- **Snowflake Integration**: Cloud data warehouse

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request
