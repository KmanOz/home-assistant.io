---
layout: component
title: "aREST binary sensor"
description: "Instructions how to integrate aREST binary sensors within Home Assistant."
date: 2015-11-20 18:15
sidebar: true
comments: false
sharing: true
footer: true
logo: arest.png
ha_category: Binary Sensor
---


The arest binary sensor platform allows you to get all data from your devices (like Arduinos with a ethernet/wifi connection, the ESP8266, and the Raspberry Pi) running the [aREST](http://arest.io/) RESTful framework.

To use your aREST binary sensor in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
binary_sensor:
  platform: arest
  resource: http://IP_ADDRESS
  name: Office Switch
  pin: 8
```

Configuration variables:

- **resource** (*Required*): IP address and schema of the device that is exposing an aREST API, e.g. http://192.168.1.10.
- **name** (*Optional*): Let you overwrite the the name of the device. By default *name* from the device is used.
- **pin** (*Required*): Number of the pin to monitor.

Accessing the URL http://IP_ADDRESS/digital/PIN_NUMBER should give you the state of the pin inside a JSON response as `return_value`.

```bash
$ curl -X GET http://10.100.0.157/digital/9
{"return_value": 0, "id": "office1", "name": "Office", "connected": true}

```

<p class='note'>
This sensor is not suitable for fast state changes because there is a high possibility that the change took place between two update cycle. 
</p>
