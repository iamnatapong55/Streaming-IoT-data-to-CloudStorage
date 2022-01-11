# Streaming IoT data to Google Cloud Storage

In this simulated project, I will configure Cloud IoT Core and Cloud Pub/Sub to create a Pub/Sub topic and registry on GCP. I will use this topic to ingest data streaming from an IoT device.

### Goal for this project
- Create Cloud Pub/Sub topics and subscriptions
- Use IoT Core to create a registry
- Start the MQTT Application on a simulator
- Stream data to Google Cloud Storage

### Methodology
1) Set up cloud account
2) Enable Cloud IoT API and Dataflow API
3) Set up Cloud Pub/Sun and create topic
4) Create a location for data storage
   4.1) Create a storage Bucket
   4.2) Create a folder in the bucket 
5) Start dataflow job

Properties        | Value.                                  |
-------------------------------------------------------------
Job name.         | sensor-data                             |
-------------------------------------------------------------
Regional endpoint | iowa                                    |
-------------------------------------------------------------
Dataflow template | Pub/Sub to Text Files on Cloud Storage. |
-------------------------------------------------------------


