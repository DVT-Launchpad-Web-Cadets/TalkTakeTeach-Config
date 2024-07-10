# TalkTakeTeach Configuration Repository

## Overview

This repository contains the configuration files and necessary setup to run the TTT's technology stack using Docker Compose. The setup is designed to facilitate easy deployment and management of the stack, with predefined volume mounts for persistent storage.

## Repository Structure

- `docker-compose.yml`: The main Docker Compose file that defines the services, networks, and volume mounts.
- `db/`: A directory containing subdirectories for mounting volumes, ensuring data persistence between container restarts.

## Directory Details

### `docker-compose.yml`

The `docker-compose.yml` file defines the following services:

- **Elasticsearch**
- **Kibana**
- **Elysia**
- **Logstash**
- **Postgres**

### `db/`

The root directory includes subdirectories for data persistence:

- `elasticsearch/`: Stores Elasticsearch data.
- `postgres/`: Stores PostgreSQL data and configurations.

## Getting Started

### Prerequisites

- Docker
- Docker Compose

### Steps to Run

1. **Clone the repository**:

   ```sh
   git clone https://github.com/DVT-Launchpad-Web-Cadets/talktaketeach-config.git
   cd talktaketeach-config
   ```

2. **Create db directories**:

   ```
   mkdir db
   mkdir db/elasticsearch
   mkdir db/postgres
   ```

3. **Build and start the services**:

   ```sh
   docker-compose up --build
   ```

4. **Setup Kibana**:

   - Exec into elasticsearch docker container and run the following commands:
     ```sh
     cd /usr/share/elasticsearch/bin
     ./elasticsearch-reset-password -u kibana_system --auto
     ```
   - Copy the password and update the password in kibana.yml
   - Stop and remove the kibana container
     ```sh
     docker stop kibana_container
     docker rm kibana_container
     ```
   - Start back up the service
     ```sh
     docker-compose up -d
     ```
   - When accessing Kibana, use the Elastic username and password
   - Create dashboard and import the saved dashboard 'logs-dashboard'

5. **Access the services**:
   - **Elasticsearch**: Accessible at `http://localhost:9200`
   - **Kibana**: Accessible at `http://localhost:5601`
   - **Postgres**: Accessible at `http://locahost:5432`
   - **Elysia**: Accessible at `http://localhost:3000`

### Customization

You can customize the `docker-compose.yml` file and the volume directories as needed. For example, you can adjust environment variables, add additional services, or change the volume paths to suit your specific requirements.
