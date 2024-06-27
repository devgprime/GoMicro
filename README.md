## GoMicro
This project aims at orchestrating a Go-powered microservices architecture with a central broker (optional) and services for authentication, logging, queue processing, and email communication.


##  Key Components:

Broker Service (Optional): Acts as a central gateway to all services, facilitating seamless communication through JSON over gRPC and RabbitMQ messaging.

Authentication Service: Secures user access by validating credentials against a Postgres database.

Logger Service: Records critical events from all services into a MongoDB database, supporting RPC, gRPC, and JSON input.

Queue Listener Service: Actively consumes messages from RabbitMQ, triggering corresponding actions based on the payload.

Mail Service: Simplifies email communication by accepting JSON input.

Service Discovery:

All services, except the broker, dynamically register their access URLs with etcd, a distributed key-value store, and maintain their availability through automatic lease renewals. This elegant mechanism enables a straightforward service discovery system, with a centralized "service map" within the broker service's configuration.

## Additional Infrastructure:

The project includes a docker-compose.yml file to effortlessly orchestrate the following supporting services:

Postgresql: Used by the authentication service for user data persistence.
MongoDB: Stores logs generated by all services.
etcd: Powers service discovery.
Mailhog: Simulates a mail server for testing the mail service's functionality.
This structured approach to microservice development in Go enhances scalability, maintainability, and resilience. Each service is focused on a specific task, making the overall system more adaptable and easier to manage.


## Project Management

```bash
make up              # Start all containers without rebuilding <br>
make down            # Stop Docker Compose <br>
make up_build        # Stop (if running), rebuild all services, and start Docker Compose <br>
make test            # Run all tests <br>
make clean           # Clean up binaries

```
## Service Management
```bash

make auth            # Rebuild and restart authentication service
make broker          # Rebuild and restart broker service
make logger          # Rebuild and restart logger service
make mail            # Rebuild and restart mail service
make listener        # Rebuild and restart listener service
