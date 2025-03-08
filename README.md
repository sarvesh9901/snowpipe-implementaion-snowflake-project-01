# Snowpipe: Automating Data Ingestion from GCP to Snowflake

## Overview
This project automates the process of loading data files from a Google Cloud Platform (GCP) bucket into a Snowflake database table using Snowpipe. The setup ensures that whenever a new file is uploaded to the GCP bucket, it is automatically ingested into Snowflake.

## Architecture
1. **GCP Bucket**: Data files are periodically uploaded to a designated GCP bucket.
2. **Snowflake Storage Integration**: Allows Snowflake to access the GCP bucket.
3. **Permissions & Roles**: A new role is created in Snowflake with necessary permissions to access the GCP bucket.
4. **GCP Pub/Sub Notification**: A Pub/Sub topic and notification are set up to detect file uploads.
5. **Snowflake Notification Integration**: Enables Snowflake to subscribe to the Pub/Sub topic and trigger Snowpipe.
6. **Snowpipe**: Automatically loads data from the GCP bucket into a Snowflake table when a new file is detected.

## Setup Instructions
### 1. Configure Snowflake Storage Integration
- Create a storage integration in Snowflake to access the GCP bucket.
- Assign the following permissions to the integration:
  - `storage.buckets.get`
  - `storage.objects.get`
  - `storage.objects.list`
- Attach the role to the GCP bucket.

### 2. Configure GCP Pub/Sub
- Create a **Pub/Sub topic** in GCP.
- Set up a **bucket notification** that publishes messages to the Pub/Sub topic whenever a new file is uploaded.

### 3. Configure Snowflake Notification Integration
- Create a **notification integration** in Snowflake that subscribes to the Pub/Sub topic.
- This integration listens for new file events and triggers Snowpipe.

### 4. Configure Snowpipe
- Create a Snowpipe in Snowflake that:
  - Monitors the Snowflake **staging area** (linked to the GCP bucket via storage integration).
  - Automatically loads new files into the target Snowflake database table.

## Workflow
1. A new file is uploaded to the GCP bucket.
2. A notification is sent to the Pub/Sub topic.
3. Snowflake's notification integration picks up the message.
4. Snowpipe is triggered and fetches the file from the GCP bucket.
5. Data is loaded into the Snowflake database table.

## Benefits
- **Real-time Data Loading**: Ensures minimal latency between file uploads and data availability in Snowflake.
- **Automated Workflow**: Eliminates manual intervention in data ingestion.
- **Scalability**: Supports continuous and large-scale data ingestion.
- **Seamless Integration**: Utilizes GCP and Snowflake's native integrations.

## Conclusion
This setup enables an efficient, automated data ingestion pipeline from GCP to Snowflake using Snowpipe, reducing operational overhead while ensuring real-time data availability.

