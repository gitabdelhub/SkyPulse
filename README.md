# SkyPulse Streaming — Real-Time Flight Intelligence Pipeline

A production-oriented starter scaffold for an end-to-end real-time flight tracking data platform using OpenSky telemetry, Kafka, Spark Structured Streaming, and a Medallion data architecture.

## High-level architecture

```mermaid
flowchart LR
  A[OpenSky REST API\nADS-B telemetry] --> B[Python Producer\nPolling + publish]
  B --> C[Apache Kafka\nRaw flight events]
  C --> D[Spark Structured Streaming\nSpeed layer processing]
  D --> E[Bronze\nRaw JSON/Parquet]
  E --> F[Silver\nCleaned Delta/Parquet]
  F --> G[Gold\nAggregated business tables]
  G --> H[(PostgreSQL / TimescaleDB)]
  G --> I[Parquet + DuckDB reports]
```

## Tech stack

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?logo=python&logoColor=white)
![Apache Kafka](https://img.shields.io/badge/Apache%20Kafka-Streaming-231F20?logo=apachekafka&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-Structured%20Streaming-E25A1C?logo=apachespark&logoColor=white)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-Medallion-0A9396)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Serving%20Layer-336791?logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Local%20Orchestration-2496ED?logo=docker&logoColor=white)

## Repository structure

```text
.
├── docker/
│   └── docker-compose.yml
├── src/
│   ├── producers/
│   ├── streaming/
│   └── batch/
├── data/
│   └── reference/
├── notebooks/
├── tests/
│   ├── unit/
│   └── integration/
├── decisions/
├── .env.example
├── .gitignore
├── requirements.txt
└── README.md
```

## Prerequisites

- Python 3.11+
- Docker + Docker Compose
- Java 11+ (required for local Spark)

## Quick start

1. **Create local environment file**
   ```bash
   cp .env.example .env
   ```
2. **Install Python dependencies**
   ```bash
   pip install -r requirements.txt
   ```
3. **Start infrastructure services**
   ```bash
   docker compose -f docker/docker-compose.yml up -d
   ```
4. **Begin implementing pipeline components**
   - `src/producers/`: OpenSky polling and Kafka producer
   - `src/streaming/`: Spark Structured Streaming transforms
   - `src/batch/`: daily gold aggregations/reporting jobs

## Notes

This repository currently provides skeleton structure and orchestration only. Business logic for ingestion and transformations is intentionally left unimplemented.
