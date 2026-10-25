# Kafka Cab Booking Demo

## Overview

This project demonstrates real-time communication between two Spring Boot microservices using Apache Kafka.

The system consists of:

1. **cabBookDriver** - Kafka Producer (Publisher)
2. **cabBookUser** - Kafka Consumer

The producer continuously generates random cab location coordinates and publishes them to a Kafka topic. The consumer subscribes to the same topic, receives the location updates, and displays them in the console in real time.

---

## Project Architecture

```text
+----------------------+
|    cabBookDriver     |
|      Publisher       |
+----------+-----------+
           |
           | Publish Messages
           v
+----------------------+
|     Kafka Topic      |
|    cab-location      |
+----------+-----------+
           |
           | Consume Messages
           v
+----------------------+
|     cabBookUser      |
|      Consumer        |
+----------------------+
```

---

## Publisher Service (cabBookDriver)

The **cabBookDriver** application acts as a Kafka Producer.

### API Endpoint

```http
GET http://localhost:8081/location
```

### Functionality

When the endpoint is invoked:

- Two random numbers are generated to represent cab location coordinates.
- Location data is generated every second.
- The process continues for 100 seconds.
- Each generated location is published to the Kafka topic:

```text
cab-location
```

### Sample Published Messages

```json
(12, 45)
```

```json
(78, 23)
```

```json
(34, 90)
```

These messages simulate live cab movement updates.

---

## Kafka Topic

The producer publishes all generated location updates to the following topic:

```text
cab-location
```

Kafka acts as a message broker between the producer and consumer applications.

---

## Consumer Service (cabBookUser)

The **cabBookUser** application acts as a Kafka Consumer.

### Functionality

- Subscribes to the Kafka topic:

```text
cab-location
```

- Receives location messages as soon as they are published by the producer.
- Prints the received locations in the console in real time.

### Sample Consumer Output

```text
Location Received : (12.656,45.52364)

Location Received : (78.676,23.5635)

Location Received : (34.4365,90.58654)

Location Received : (67.657,12.6745)
```

---

## Application Workflow

### Step 1

Start Zookeeper and Kafka Server.

### Step 2

Run the **cabBookDriver** application.

### Step 3

Run the **cabBookUser** application.

### Step 4

Invoke the Producer API:

```http
http://localhost:8081/location
```

### Step 5

The Producer generates random location coordinates every second for 100 seconds.

Example:

```text
(10.5345,25)
(14.09234,32.6443)
(22.6544,41.635)
(29.89354,47.6256)
...
```

### Step 6

Each location update is published to the Kafka Topic:

```text
cab-location
```

### Step 7

The Consumer receives the published messages and prints them to the console.

---

## Data Flow Example

```text
Producer (cabBookDriver)
        |
        |  (25.53832,40.3933)
        |
        v
Kafka Topic (cab-location)
        |
        |  (25.0904,40.9734)
        |
        v
Consumer (cabBookUser)

Console Output:
Location Received : (25.073,40.67543)
```

---

## Technologies Used

- Java
- Spring Boot
- Apache Kafka
- Kafka Producer
- Kafka Consumer
- REST API
- Maven

---

## Key Features

✅ Real-time Message Publishing

✅ Kafka Producer Implementation

✅ Kafka Consumer Implementation

✅ Topic-based Communication

✅ Event-Driven Architecture

✅ Asynchronous Processing

✅ Spring Boot Microservices

---

## Conclusion

This project demonstrates an event-driven architecture using Apache Kafka, where the **cabBookDriver** service publishes live cab location updates to the **cab-location** topic and the **cabBookUser** service consumes those updates in real time.

It provides a simple and effective example of Producer-Consumer communication using Spring Boot and Apache Kafka.
