# Airflow ETL Project

This project is an ETL (Extract, Transform, Load) pipeline built with Apache Airflow. It extracts weather data from the Open-Meteo API, transforms it, and loads it into a PostgreSQL database.

## Project Structure

- `dags/`: Contains the Airflow DAGs (Directed Acyclic Graphs).
  - `etl_weather.py`: The main ETL pipeline for weather data.
  - `exampledag.py`: An example DAG that fetches data about astronauts in space.
- `include/`: Can be used to store additional files required by the DAGs.
- `plugins/`: Can be used for custom Airflow plugins.
- `tests/`: Contains tests for the DAGs.
- `.dockerignore`: Specifies files to ignore when building the Docker image.
- `docker-compose.yml`: Defines the services for the Airflow environment, including Postgres, the Airflow webserver, and the scheduler.
- `Dockerfile`: Defines the custom Docker image for the Airflow environment.
- `packages.txt`: Lists system-level dependencies required for the Docker image.
- `requirements.txt`: Lists the Python dependencies for the project.

## Prerequisites

- [Docker](https://www.docker.com/get-started)
- [Astro CLI](https://docs.astronomer.io/astro/cli/install-cli)

## Getting Started

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd airflow_etl
   ```

2. **Set up Airflow Connections:**

   This project requires two Airflow connections to be set up:

   - **`open_meteo_api`**: An HTTP connection for the Open-Meteo weather API.
     - **Conn ID:** `open_meteo_api`
     - **Conn Type:** `HTTP`
     - **Host:** `https://api.open-meteo.com`

   - **`postgress_default`**: A Postgres connection for the database.
     - **Conn ID:** `postgress_default`
     - **Conn Type:** `Postgres`
     - **Host:** `postgres`
     - **Login:** `airflow`
     - **Password:** `airflow`
     - **Schema:** `airflow`


   You can set these up in the Airflow UI under **Admin -> Connections**.

3. **Start the Airflow environment:**

   ```bash
   astro dev start
   ```

   This command will build the Docker images and start all the necessary services.

4. **Access the Airflow UI:**

   Once the environment is running, you can access the Airflow UI at `http://localhost:8080`. The default credentials are:
   - **Username:** `admin`
   - **Password:** `admin`

5. **Enable the DAGs:**

   In the Airflow UI, you will see the `weather_etl_pipeline` and `example_astronauts` DAGs. You can enable them by toggling the switch next to their names.

## DAGs

- **`weather_etl_pipeline`**: This DAG runs daily, extracts current weather data for a predefined latitude and longitude, transforms the data, and loads it into a `weather_data` table in the Postgres database.

- **`example_astronauts`**: This is an example DAG that fetches the number of astronauts currently in space from the Open Notify API and prints their names and the spacecraft they are on.
