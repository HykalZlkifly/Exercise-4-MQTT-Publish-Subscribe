# 📡 MQTT Publish/Subscribe Lab (Node-RED + EMQX)

## 📌 Overview

This lab demonstrates the **MQTT publish-subscribe architecture** using an enterprise-grade broker (**EMQX**), Node-RED, and Postman.

Unlike HTTP (request-response), MQTT enables **real-time, event-driven communication** between devices using topics.

---

## 🎯 Objectives

* Deploy an MQTT broker using Docker (EMQX)
* Configure Node-RED as an MQTT publisher
* Use Postman as an MQTT subscriber
* Understand topic-based communication
* Explore MQTT wildcards (`#` and `+`)

---

## 🧰 Tools & Technologies

* Docker Desktop
* EMQX MQTT Broker
* Node-RED
* Postman
* JSON

---

## 🧪 System Architecture

```id="arch-flow"
Node-RED (Publisher)
        ↓
   EMQX Broker
        ↓
Postman (Subscriber)
```

---

## 🧪 Part 1: MQTT Broker Setup (EMQX)

### 🔹 Steps:

1. Run EMQX using Docker
2. Expose required ports:

```id="ports"
18083, 1883, 8083, 8080, 8883
```

3. Access dashboard:

```id="dashboard"
http://localhost:18083
```

### 📌 Function:

* Acts as a **middleman**
* Receives messages from publishers
* Distributes messages to subscribers

---

## 🧪 Part 2: Node-RED as Publisher

### 🔹 Configuration:

* Inject node (every 5 seconds)
* JSON payload:

```json id="payload"
{
  "temperature": 25.5,
  "sensor": "ESP32_01"
}
```

* MQTT topic:

```id="topic"
campus/lab1/temperature
```

### 📌 Function:

* Simulates IoT sensor
* Publishes data continuously to broker

---

## 🧪 Part 3: Postman as Subscriber

### 🔹 Configuration:

* Connect to:

```id="broker"
mqtt://localhost:1883
```

* Subscribe to:

```id="sub-topic"
campus/lab1/temperature
```

### 📌 Function:

* Listens to topic
* Displays incoming data in real-time

---

## 🧪 Part 4: Topic Hierarchy & Wildcards

### 🔹 Topics Used:

```id="topics"
campus/lab1/temperature
campus/lab2/temperature
campus/lab1/humidity
```

---

### 🔹 Multi-Level Wildcard (`#`)

```id="multi"
campus/#
```

📌 Result:

* Receives **ALL topics under campus**

---

### 🔹 Single-Level Wildcard (`+`)

```id="single"
campus/+/temperature
```

📌 Result:

* Receives:

  * lab1 temperature
  * lab2 temperature
* ❌ Does NOT receive humidity

---

## ⚡ Key Concepts

### 🔹 Publisher

* Sends data to topic
* Example: Node-RED

### 🔹 Subscriber

* Receives data from topic
* Example: Postman

### 🔹 Broker

* Connects publishers and subscribers
* Example: EMQX

---

## 🔥 MQTT vs HTTP

| Feature       | MQTT              | HTTP                |
| ------------- | ----------------- | ------------------- |
| Communication | Publish-Subscribe | Request-Response    |
| Efficiency    | Lightweight       | Higher overhead     |
| Real-time     | Yes               | No (polling needed) |
| Coupling      | Loose             | Tight               |

---

## ⚠️ Key Insight

* MQTT enables **real-time IoT communication**
* Devices do **not need direct connection**
* More efficient than HTTP for sensor data

---

## 📚 Conclusion

This lab shows how MQTT improves IoT communication by using a broker-based architecture.
It enables scalable, efficient, and real-time data exchange between devices.

---
