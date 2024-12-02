# Neo4j for BloodHound - Docker Compose

This repository provides a simple Docker Compose setup for running Neo4j, configured for BloodHound. It enables remote access for both the HTTP web interface and the Bolt protocol, making it easy to integrate with BloodHound.

## Features
- **Neo4j 4.4**: Lightweight and compatible version for BloodHound.
- **Remote Access**: Accessible from devices other than `localhost`.
- **Persistent Storage**: Uses Docker volumes to retain data, logs, and plugins.

## Setup

1. Clone this repository:
   ```bash
   git clone https://github.com/ReanSchwarzer9029/neo4j-bloodhound.git
   cd neo4j-bloodhound
   ```

2. Start the Neo4j container:
   ```bash
   docker-compose up -d
   ```

3. Access the Neo4j web interface:
   - URL: `http://<host-IP>:7474`
   - Login: `neo4j`
   - Password: `changeme`

4. Connect BloodHound:
   - Bolt URL: `bolt://<host-IP>:7687`
   - Login: `neo4j`
   - Password: `changeme`

## Customization

- Change the default password by modifying `NEO4J_AUTH` in `docker-compose.yml`:
  ```yaml
  environment:
    - NEO4J_AUTH=neo4j/changeme
  ```

## Volumes

The following volumes are used for data persistence:
- `neo4j_data`: Stores the database files.
- `neo4j_logs`: Stores log files.
- `neo4j_import`: For importing data.
- `neo4j_plugins`: For custom plugins.

## Stop and Clean Up
To stop and remove the container:
```bash
docker-compose down
```

To remove all volumes:
```bash
docker volume rm neo4j_data neo4j_logs neo4j_import neo4j_plugins
```

## Notes
- Ensure the Docker host's IP is accessible from your network.
- Update firewall rules if required to allow access to ports `7474` and `7687`.