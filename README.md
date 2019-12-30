# iot-gcp-firebase

## Description 
**iot-store-display** hosts the Firebase aspects of **an IoT project** relying on [GCP-Cloud IoT Core](https://cloud.google.com/iot-core/). We called our GCP project **hello-cloud-iot-core**.

**Devices** publish weather data messages to a **telemetry topic** connected to the MQTT bridge of Cloud Iot Core.

A device is an [ESP32](https://www.espressif.com/en/products/hardware/esp32/overview) Wifi chip associated with a DHT22 temperature/humidity sensor. The ESP32 runs [Mongoose OS](https://mongoose-os.com/).

All data messages are then forwarded to a **Cloud Pub/Sub** topic of the project and this is where the files in this repository intervene:
* A **Cloud Function for Firebase** is triggered upon a publication to the Cloud Pub/Sub topic. Its aim is to log the last weather data as it is published and also to store it in a **Firebase Realtime Database**. The Cloud Function implementation is the `index.js` file, hosted in the [functions](functions) directory.
* The read/write rules of this database are described in the `database.rules.json` file.
* A **web app** hosted by **Firebase Hosting** is in charge of plotting the *n* last weather data each time a new data arrives in the Realtime Database. The files for this web app are hosted in the [public](public) directory.
