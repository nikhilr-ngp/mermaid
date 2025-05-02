``` mermaid
graph TD
    A[Smart Metering & Pricing ETL Pipeline]
    
    A --> B1[Data Ingestion]
    A --> B2[Data Processing]
    A --> B3[Forecasting & API]
    A --> B4[Visualization]
    A --> B5[User Access & Auth]
    A --> B6[Monitoring & Logs]
    
    B1 --> C1a[RabbitMQ Streaming]
    C1a --> C1b[Gmail Tariff Ingestion]
    C1b --> C1c[Cloud Storage GCS]
    
    B2 --> C2a[Airflow DAG Scheduling]
    B2 --> C2b[DBT Transformation]
    B2 --> C2c[Validation & Cleansing]
    
    B3 --> C3a[Flask REST APIs]
    B3 --> C3b[Pricing Forecast Module]
    B3 --> C3c[Historical Query Handler]
    
    B4 --> C4a[Looker Studio Dashboards]
    B4 --> C4b[Vue.js Frontend]
    B4 --> C4c[Role-Based Views]
    
    B5 --> C5a[Login / Signup]
    B5 --> C5b[OAuth 2.0 Integration]
    B5 --> C5c[Session Handling]
    
    B6 --> C6a[Error Logging]
    B6 --> C6b[DAG Monitoring]
    B6 --> C6c[Alert Notifications]

```

```

flowchart TD
    A(Electric Meter) -->|Real-time sync| B(API Calls)
    A -->|Batch transfer| C(FTP Server)
    B --> D(RabbitMQ)
    C --> E(Google Cloud Storage)
    D --> E
    F(Gmail Supplier Files) --> E

    E --> G(Airflow Scheduler)
    G --> H(dbt Models)
    H --> I(BigQuery)

    I --> J(Price Book Agent View)
    I --> K(Looker Studio Dashboards)

```

```
classDiagram
    class ElectricMeter {
        +String meterId
        +Decimal voltage
        +Decimal current
        +Decimal power
        +Decimal powerFactor
    }
    class API {
        +Fetch real-time data
    }
    class FTPServer {
        +Batch upload files
    }
    class RabbitMQ {
        +Queue real-time data
    }
    class GoogleCloudStorage {
        +Store raw energy data
        +Store supplier files
    }
    class Airflow {
        +Orchestrate ETL workflows
    }
    class dbtModel {
        +Transform and clean data
    }
    class BigQuery {
        +Store analytics-ready data
    }
    class LookerStudio {
        +Visualize consumption and pricing
    }
    class PriceBook {
        +Display supplier prices
    }

    ElectricMeter --> API
    ElectricMeter --> FTPServer
    API --> RabbitMQ
    RabbitMQ --> GoogleCloudStorage
    FTPServer --> GoogleCloudStorage
    GoogleCloudStorage --> Airflow
    Airflow --> dbtModel
    dbtModel --> BigQuery
    BigQuery --> LookerStudio
    BigQuery --> PriceBook

```
