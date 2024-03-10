# AdvertiseX Data Engineering Solution

## Overview

This repository contains a data engineering solution for AdvertiseX, a digital advertising technology company specializing in programmatic advertising. The solution addresses challenges related to data sources, formats, ingestion, processing, storage, and monitoring.

## Table of Contents

- [Data Sources and Formats](#data-sources-and-formats)
- [Case Study Requirements](#case-study-requirements)
- [Solution Overview](#solution-overview)
- [Usage](#usage)
- [Requirements](#requirements)

## Data Sources and Formats

1. **Ad Impressions:**
   - Data Source: AdvertiseX serves digital ads to various online platforms and websites.
   - Data Format: Ad impressions data is generated in JSON format, containing information such as ad creative ID, user ID, timestamp, and the website where the ad was displayed.

2. **Clicks and Conversions:**
   - Data Source: AdvertiseX tracks user interactions with ads, including clicks and conversions.
   - Data Format: Click and conversion data is logged in CSV format and includes event timestamps, user IDs, ad campaign IDs, and conversion type.

3. **Bid Requests:**
   - Data Source: AdvertiseX participates in real-time bidding (RTB) auctions.
   - Data Format: Bid request data is received in a semi-structured format, mostly in Avro, and includes user information, auction details, and ad targeting criteria.

## Case Study Requirements

1. **Data Ingestion:**
   - Implement a scalable data ingestion system capable of collecting and processing ad impressions (JSON), clicks/conversions (CSV), and bid requests (Avro) data.
   - Ensure that the ingestion system can handle high data volumes generated in real-time and batch modes.

2. **Data Processing:**
   - Develop data transformation processes to standardize and enrich the data. Handle data validation, filtering, and deduplication.
   - Implement logic to correlate ad impressions with clicks and conversions to provide meaningful insights.

3. **Data Storage and Query Performance:**
   - Select an appropriate data storage solution for storing processed data efficiently, enabling fast querying for campaign performance analysis.
   - Optimize the storage system for analytical queries and aggregations of ad campaign data.

4. **Error Handling and Monitoring:**
   - Create an error handling and monitoring system to detect data anomalies, discrepancies, or delays.
   - Implement alerting mechanisms to address data quality issues in real-time, ensuring that discrepancies are resolved promptly to maintain ad campaign effectiveness.

## Solution Overview

### Database Models (models.py)

- Defines Cassandra models for User, Website, Ads, Clicks, Impression, and Bid.

### Data Ingestion (producer.py)

- Produces simulated data for users, websites, ads, impressions, clicks, and bids to Kafka topics.
- Uses Avro schema for bid data and CSV format for click data.

### Data Consumption (consumer.py)

- Consumes data from Kafka topics and inserts into Cassandra tables.
- Implements separate functions for consuming user, website, ads, impressions, clicks, and bids data.
- Utilizes Avro and CSV parsing for bid and click data, respectively.

### Execution

- Execute the `producer.py -n [num of messages]` or `producer.py --number [num of messages]` script to simulate data production.
- Run the `consumer.py` script to consume and store data in the Cassandra database.

## Usage

1. Run Cassandra Container using Docker
    ```bash
    docker run --name cassandra-container -p 9042:9042 -d cassandra:latest
    ```
2. Start local kafka cluster:
    ```bash
    confluent local kafka start
    ```
    update the port details and broker addresses in the `config/config.py`
3. Create virtual environment:
    ```bash
    virtualenv env
    ```
    activate the virtual environment:
    ```bash
    source env/bin/activate
    ```
4. Install dependencies: 
    ```bash
    pip install -r requirements.txt
    ```
5. Execute the scripts: 
    Run `kafka/producer.py -n [num of messages]` to produce data and `kafka/consumer.py` to consume and store data.

## Requirements

- Python 3.x
- Apache Kafka
- Apache Cassandra
- Docker
