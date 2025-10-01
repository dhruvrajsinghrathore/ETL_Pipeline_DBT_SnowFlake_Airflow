# ETL Pipeline with dbt, Snowflake, and Airflow

This project implements a complete ETL pipeline using:
- **dbt** for data transformation
- **Snowflake** as the data warehouse
- **Airflow** for orchestration

## Project Structure

```
ETL_pipeline_DBT_Snowflake_Airflow/
├── dbt_dag/                    # Airflow DAGs and dbt project
│   ├── dags/                   # Airflow DAG files
│   │   ├── dbt_dag.py         # Main dbt orchestration DAG
│   │   └── dbt/                # dbt project directory
│   │       └── data_pipeline/  # dbt project
│   │           ├── models/
│   │           │   ├── staging/    # Staging models
│   │           │   └── marts/      # Mart models
│   │           ├── tests/          # dbt tests
│   │           ├── macros/         # dbt macros
│   │           ├── dbt_project.yml # dbt configuration
│   │           └── packages.yml    # dbt packages
│   ├── requirements.txt        # Python dependencies
│   └── Dockerfile             # Docker configuration
└── .gitignore                 # Git ignore rules
```

## Setup Instructions

### Prerequisites
- Python 3.8+
- Docker
- Snowflake account
- Airflow (Astro CLI recommended)

### 1. Setup Airflow Environment
```bash
cd dbt_dag
astro dev start
```

### 2. Configure Snowflake Connection in Airflow
1. Go to Airflow UI (usually http://localhost:8080)
2. Navigate to Admin > Connections
3. Create a new connection with ID `snowflake_conn`
4. Set connection type to `Snowflake`
5. Add your Snowflake credentials in the Extra field:
```json
{
  "account": "your_account",
  "user": "your_username",
  "role": "your_role",
  "warehouse": "your_warehouse",
  "database": "your_database",
  "schema": "your_schema"
}
```

### 3. Run dbt Models via Airflow
The dbt models will be automatically executed by the Airflow DAG on a daily schedule.

### 4. Manual dbt Execution (Optional)
If you want to run dbt models manually:
```bash
cd dbt_dag/dags/dbt/data_pipeline
dbt run
dbt test
```

## Features

- **Integrated Architecture**: dbt project embedded within Airflow DAGs
- **Staging Models**: Raw data transformation from Snowflake sample data
- **Mart Models**: Business-ready data marts (orders, line items)
- **Data Tests**: Automated data quality checks
- **Airflow Orchestration**: Scheduled pipeline execution with Cosmos
- **Snowflake Integration**: Cloud data warehouse with TPC-H sample data
- **Docker Support**: Containerized deployment ready

## DAG Configuration

The main DAG (`dbt_dag.py`) uses Cosmos to orchestrate dbt models:
- **Schedule**: Daily execution
- **dbt Project Path**: `/usr/local/airflow/dags/dbt/data_pipeline`
- **Profile**: Uses Airflow connection `snowflake_conn`
- **Dependencies**: Automatically installs dbt packages

## Data Sources

This pipeline processes TPC-H sample data from Snowflake:
- **Source Database**: `snowflake_sample_data`
- **Source Schema**: `tpch_sf1`
- **Tables**: `orders`, `lineitem`

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

MIT License - see [LICENSE](LICENSE) file for details.
