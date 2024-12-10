# Kong API Gateway with Deck Integration

This repository contains resources for setting up and configuring the **Kong API Gateway** using Docker Compose and **Deck** for configuration management.

---

## Project Structure

- `docker-compose.yaml`: Docker Compose file to set up Kong API Gateway, PostgreSQL database, and Konga (a Kong GUI).
- `example-kong-deck.yml`: Configuration file for Kong API Gateway, including service and route definitions, managed using Deck.

---

## Prerequisites

- Docker and Docker Compose installed on your system.
- An environment capable of running Deck CLI (for example, Linux or macOS with `deck` installed).

---

## Environment Variables

The following environment variables can be set to customize the deployment:

- `KONG_DOCKER_TAG`: Tag for the Kong Docker image (default: `kong:latest`).
- `KONG_PG_DATABASE`: Name of the PostgreSQL database for Kong (default: `kong`).
- `KONG_PG_USER`: Username for PostgreSQL (default: `kong`).
- `KONG_PG_PASSWORD`: Password for PostgreSQL (default: `kong`).

You can create a `.env` file in the root of the repository to set these variables.

---

## Quickstart

### Step 1: Start the Kong Environment

1. Clone this repository:
   ```bash
   git clone <repository_url>
   cd <repository_directory>

2. Start the Kong stack:
`docker-compose up -d`

3. Verify the services are running:
   - Kong Admin: http://localhost:8001
   - Kong Proxy: http://localhost:8800
   - Kong GUI: http://localhost:1337
  
### Step 2: Apply Configuration Using Deck
1. Ensure the deck CLI is installed:
   `deck version`
2. Apply the configuration from example-kong-deck.yml:
   `deck sync -s example-kong-deck.yml`
3. Verify the configurations have been applied:
   `deck list services`
   `deck list routes`
## Explanation of Services 

### Kong API Gateway
Manages the routing of API requests and applies transformations as defined in the configuration

### PostgreSQL Database
Acts as the datastore for Kong to persist configurations.

### Konga
Provides a GUI for managing Kong configurations.


## Configuration Details
The file `example-kong-deck.yml` defines two primary services with routes:
1. **Transactions_API_of_BanKonG**
   - Routes for transaction-related APIs (GET, POST, PATCH, DELETE).
2. **Mockbin_API_of_BanKonG**
   - A route to test and debug APIs with an echo service.

### Environment Variables in Deck Configuration
Deck configuration leverages environment variables for flexibility. Ensure the `DECK_FQDN` variable is set before applying the configuration.

## Cleanup
To stop and remove the services:
`docker-compose down -v`

## Troubleshooting
- **Database Connection Issues: Ensure the `POSTGRES_PASSWORD`, `POSTGRES_USER`, and `POSTGRES_DB` are consistent between the `docker-compose.yaml` and your `.env` file.**
- **Deck Sync Errors: Verify the `KONG_ADMIN_LISTEN` and `DECK_FQDN` values in your setup.**
