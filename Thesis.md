``` mermaid
flowchart TD
    Start([Start]) --> IngestAPI[Ingest real-time data via API]
    Start --> IngestBatch[Ingest batch data via FTP]
    IngestAPI --> StoreGCS[Store raw data in Google Cloud Storage]
    IngestBatch --> StoreGCS
    SupplierPricing[Extract Supplier Pricing from Gmail] --> StoreGCS

    StoreGCS --> AirflowTrigger[Trigger Airflow Workflow]
    AirflowTrigger --> dbtRun[Run dbt Models for Transformation]
    dbtRun --> LoadBigQuery[Load Transformed Data to BigQuery]

    LoadBigQuery --> UpdatePriceBook[Update Price Book View]
    LoadBigQuery --> RefreshLooker[Refresh Looker Studio Dashboards]
    UpdatePriceBook --> End([End])
    RefreshLooker --> End
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
