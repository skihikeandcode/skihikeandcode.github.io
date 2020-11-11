---
layout: post
title:  "MQTT Basic"
category: "IoT"
---

# Overview

MQTT is a lightweight publish/subscribe messaging protocol designed for M2M(machine to machine) telemetry in low bandwidth environments. It was designed by Andy Standford-Clark (IBM) and Arlen Nipper in 1999 for connecting Oil Pipeline telemetry systems over satellite. It was released Royalty free in 2010 and became OASIS standard in 2014. MQTT is fast becoming one of main protocols for IoT deployments.<br>

# MQTT version

## MQTT

There are two versions of MQTT. The original MQTT which was designed in 1999 and has been in use for many years. It was designed for TCP/IP networks.

## MQTT-SN

It was specified in around 2013, and designed to work over UDP, ZigBee and other transports.

# MQTT Basics - How MQTT works

MQTT uses a publish/subscribe model which requires the use of **a central broker**. The model is similar to broadcast radio and TV where a TV or radio station broadcasts on a channel and listeners/viewers tune in to that channel. In this model there is **no direct connection** between a publisher and subscriber. However unlike the broadcast TV/radio model, in MQTT all clients can publish (broadcast) and subscribe(receive). Instead of channels MQTT uses **Topics**.

# MQTT Topics

These are like channels in the TV radio model. Topics are what connect the publisher and subscriber. In MQTT there is **no formal structure** and a publisher is free to choose it's own topic names and structure.

## What Happens to Published Messages

When a client publishes a message on a topic then the broker will distribute that message to any connected clients that have subscribed to that topic. Once the message has been sent to those clients it is removed from the broker. If no clients have subscribed to the topic or they aren't currently connected then the message is immediately removed from the broker. In general **the broker doesn't store messages**. 

# MQTT QoS Levels

Networks are unreliable and MQTT lets you select from three QoS levels depending on your requirements. If your application can tolerate lost or missing messages then you can choose the lowest level **QoS 0** Other wise you will need to use QoS level 1 (at least once) or QoS level 2 (at most once) The higher the QoS level the more overhead is involved.

# MQTT Brokers and Servers

**Note:** The original term was broker but it has now been standardized as server.

There are many MQTT brokers available that you can use for testing and for real applications. There are free self hosted brokers, the most popular being Mosquitto and commercial ones like HiveMQ. Mosquitto is a free open source MQTT broker that runs on Windows and Linux. There is also a cloud based broker. Ecipse has a free public MQTT broker and COAP server. The address is iot.eclipse.org and the port is 1883 or 8883(SSL).

# MQTT Clients

Because MQTT clients don't have addresses, you don't need to assign addresses to clients like you do with most messaging systems. There is client software available in almost all programming languages and for the main operating systems like Linux, Windows, Mac from the Eclipse Paho project.  

---

# MQTT-SN

MQTT-SN(MQTT for sensor networks) was designed specifically to work on wireless networks. The main characteristics of these networks that drove the design are:

* Low power battery operated sensors with very limited processing power and storage
* Limited payload size
* Not always on (sleeping)

MQTT-SN is designed, as far as possible, to work in the same way as MQTT.

## MQTT-SN vs MQTT

The main differences involve **reducing the size of the message payload** and removing the need for a permanent connection by using **UDP** as the transport protocol.

The MQTT-SN specification lists these differences.

* Connect message split into three messages. Two are optional and are used for the will message
* Topic id's used in place of topic names
* Short topic names
* Pre-defined topics
* Discovery process to let clients discover the Gateway
* Will topic and messages can be changed during the session
* Offline keep alive procedure for sleeping clients

## Architecture and Components

The specification lists three components:

* MQTT-SN Client
* MQTT-SN Gateway (Transparent Gateway or Aggregating Gateway)
* MQTT-SN forwarder

## Subscribing to MQTT-SN Topics

You can subscribe to a topics using 3 different formats:

* A long topic names as per MQTT e.g. *house/sensor1*
* A short topic name of 2 characters e.g. *s1*
* A pre-defined topic id (integer) e.g. 1

Wildcards can be used as per MQTT, but they only make sense for long topic names.

Note: Pre-defined topics are defined on the Gateway and client using a list.

 
## Publishing Messages with and Established Connection

(same to the subscribing)

## Gateway Discovery

## Topic Registration


You can publish messages without first creating a connection by using QoS of -1 or 3. 

---


# References
[1] http://www.steves-internet-guide.com/mqtt/