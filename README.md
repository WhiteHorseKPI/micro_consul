# Microservices on Flask with Hazelcast and Consul using

A demo microservices stack using **Flask**, **Consul**, **Hazelcast**, and **RabbitMQ**, showcasing service discovery, distributed configuration, messaging, and state sharing.

## Architecture & Components

- **Consul**: Provides service registration, discovery, and configuration via KV store  
- **Hazelcast**: In-memory data grid to share state (maps) across service instances  
- **RabbitMQ**: Message broker for asynchronous communication  
- **Flask services**:
  - `facade_service`: API gateway / entrypoint  
  - `logging_service`: Consumes logs / events  
  - `messages_service`: Handles messaging logic  

## Getting Started

### Prerequisites  
- Docker & Docker Compose installed  
- (Optional) Python 3 if you want to run services locally  

### Quick start  

1. **Bring up infrastructure**  
   ```bash
   docker-compose up hz1 hz2 hz3 consul-server consul-client rabbitmq
2. Launch application services
   ```bash
   docker-compose up --build facade_service logging_service_1 logging_service_2 logging_service_3 messages_service_1 messages_service_2
3. Configuration (Consul KV)
Set key/value entries under Consul KV, for example:
   ```
   rabbit_host : "rabbitmq"
   queue : "mq_for_messages_service"
   map : "distr_map"
   hazelcast_addrs : "hz1:5701,hz2:5701,hz3:5701"
   ```
4. Test with HTTP / Python client
Use http-requests.py or your own HTTP client to send requests via `facade_service`, which coordinates with downstream services.
