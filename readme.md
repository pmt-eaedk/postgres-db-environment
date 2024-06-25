# Postgres DB Environment

This repository provides a simple setup to quickly spin up a PostgreSQL database environment using Docker. It is intended for testing purposes and to facilitate development without the need for installing PostgreSQL directly on your machine.

## Contents

- `.env.sample`: The sample `.env` file, follow the format for creating and fill it up.
- `docker-compose.yml`: The Docker Compose file that defines the PostgreSQL service.
- `readme.md`: This documentation file.

## Getting Started

### Prerequisites

- [Docker](https://www.docker.com/products/docker-desktop) installed on your machine.
- [Docker Compose](https://docs.docker.com/compose/install/) installed.

### Setup

1. Clone the repository:

   ```bash
   git clone https://github.com/pmt-eaedk/postgres-db-environment.git
   cd postgres-db-environment
   ```

2. Create a `.env` file in the root directory of the repository with the following content:

   ```env
   POSTGRES_DB=your_db
   POSTGRES_USER=your_user
   POSTGRES_PASSWORD=your_password
   DATABASE_URL=postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@db:5432/${POSTGRES_DB}
   ```

   Replace `your_db`, `your_user`, and `your_password` with your desired database name, username, and password.

### Starting the Database

1. Start the PostgreSQL service using Docker Compose:

   ```bash
   docker-compose up -d
   ```

   This will pull the necessary Docker images (if not already available) and start the PostgreSQL container in detached mode.

2. Verify that the container is running:

   ```bash
   docker-compose ps
   ```

   You should see an entry for the `db` service with a status of `Up`.

### Basic Commands

1. Access the PostgreSQL database:

   ```bash
   docker-compose exec db psql -U your_user -d your_db
   ```

   This will open a PostgreSQL shell where you can run SQL commands.

2. Create a sample table and insert some data to verify the setup:

   ```sql
   CREATE TABLE test_table (
       id SERIAL PRIMARY KEY,
       name VARCHAR(50)
   );

   INSERT INTO test_table (name) VALUES ('Test Name');
   ```

3. Query the table to check if the data was inserted correctly:

   ```sql
   SELECT * FROM test_table;
   ```

   You should see the data you inserted in the previous step.

### Stopping the Database

1. Stop the PostgreSQL service:

   ```bash
   docker-compose down
   ```

   This will stop and remove the container, but the data will be persisted in the Docker volume.

## Troubleshooting

- If you encounter issues with the database not starting, ensure that there are no other services running on port `5432`.
- Verify that the environment variables in the `.env` file are correctly set.

## Additional Resources

- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
