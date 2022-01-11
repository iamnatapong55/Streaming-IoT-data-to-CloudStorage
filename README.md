# Streaming IoT data to Google Cloud Storage

In this simulated project, I will configure Cloud IoT Core and Cloud Pub/Sub to create a Pub/Sub topic and registry on GCP. I will use this topic to ingest data streaming from an IoT device.

## Goal for this project
- Create Cloud Pub/Sub topics and subscriptions
- Use IoT Core to create a registry
- Start the MQTT Application on a simulator
- Stream data to Google Cloud Storage

## Methodology

### 1) Set up cloud account
### 2) Enable Cloud IoT API and Dataflow API
### 3) Set up Cloud Pub/Sun and create topic
### 4) Create a location for data storage
   ### 4.1) Create a storage Bucket
   ### 4.2) Create a folder in the bucket 
### 5) Start dataflow job

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

8) Open Core IoT and create registry

![Picture4](https://user-images.githubusercontent.com/61028063/148890651-418d04cf-6d0d-47f3-91d2-9f65a4d87492.png)

9) Create a Cryptographic Keypair

In the SSH session on the iot-device-simulator VM instance, use these commands to create the keypair in the appropriate directory:

"cd $HOME/training-data-analyst/quests/iotlab/
openssl req -x509 -newkey rsa:2048 -keyout rsa_private.pem \
    -nodes -out rsa_cert.pem -subj "/CN=unused"

This openssl command creates an RSA cryptographic keypair and writes it to a file called rsa_private.pem

10) Create the device and add it to the registry

Device 1

Property	          | Value                      |
-------------------|----------------------------|
Device ID	       | temp-sensor-buenos-aires   |
Authentication	    | Enter manually             |
Public key format	 | RS256_X509                 |
Public key value	 | Paste the certificate      |

Device 2

Property	          | Value                      |
-------------------|----------------------------|
Device ID	       | temp-sensor-istanbul       |
Authentication	    | Enter manually             |
Public key format	 | RS256_X509                 |
Public key value	 | Paste the certificate      |

11) Run Simulated Devices

<img width="468" alt="Picture5" src="https://user-images.githubusercontent.com/61028063/148891382-d4001922-4a5c-4ac1-a3b4-7b57ca00ecd1.png">


Telemetry data will flow from the simulated devices through Cloud IoT Core to the Cloud Pub/Sub topic. In turn, the Dataflow job will read messages from the Pub/Sub topic and write their contents to GCS bucket.

12) Examine the stored data

![Picture6](https://user-images.githubusercontent.com/61028063/148891587-b02d2679-53dd-4cac-8b40-e05cff1dc122.png)

<img width="300" alt="Picture7" src="https://user-images.githubusercontent.com/61028063/148891600-18248034-0a96-4062-ad6a-ac4c66e5b96f.png">

![Picture8](https://user-images.githubusercontent.com/61028063/148891612-2fc077f9-ad97-4fbc-a401-a5ffa33dbd67.png)

13) Stop the Dataflow job

![Picture9](https://user-images.githubusercontent.com/61028063/148891704-a643a4ed-0db6-409f-b7bd-45aad673f027.png)


