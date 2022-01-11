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

Properties        | Value                                   |
------------------|-----------------------------------------|
Job name          | sensor-data                             |
Regional endpoint | iowa                                    |
Dataflow template | Pub/Sub to Text Files on Cloud Storage. |


Properties                             | Value                                |
---------------------------------------|--------------------------------------|
Input Pub/Sub topic                    | projects/my-project-id/topics/iotlab |
Output file directory in Cloud Storage |  gs://iot-data-bucket/Sensor-Data/   |
Output filename prefix                 | output-                              |
Temporary location                     | gs/:iot-data-bucket/tmp              |

6) Run Job!

![Picture2](https://user-images.githubusercontent.com/61028063/148889903-73e9a68b-1003-4e7d-8cb3-c59eeed0c990.png)


7) Prepare the Compute Engine VM

In this project, a pre-provisioned VM instance named iot-device-simulator will let me run instances of a Python script that emulate an MQTT-connected IoT device. Before I emulate the devices, I will also use this VM instance to populate the Cloud IoT Core device registry.

![Picture3](https://user-images.githubusercontent.com/61028063/148890362-a2a67a48-242c-4f02-86de-3eb7f118bb3c.png)





