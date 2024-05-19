
  <h3 align="center">Log Capture & Inspection</h3>

  <p align="center">
    Scalabe and Multi-threaded Go Backend for ingesting bulk logs, logs from different services, and also via a direct HTTP log publisher endpoint, all with advanced analytics filtering and a clean UI Interface.
    <br />
  </p>

<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation--usage">Installation & usage</a></li>
      </ul>
    </li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->

## About The Project

This solution provides a Scalable and Efficient implementation for log ingestion and analysis, leveraging the Light-weight multithreading power of Golang and search-indexing capability of ElasticSearch for effective log ingestion, storage, and analysis. It is capable of accepting logs from two distinct sources: a Kafka queue(that moves down to taking logs from various different Services) or direct HTTP API requests. It also offers a web-based user interface for log analysis, supporting various filters and search queries including regex.
![image](https://github.com/anmolchhabra21/log-capture-analysis/assets/93809908/f8bddd6d-2b02-4fc8-b33b-71284ff6e59f)


### Features

- Kafka queue for streamlined Log processing
- Regular expression search on all fields
- Text-search across all fields
- Efficient search queries leveraging Elastic DB
- Scalable & Efficient Storage using sharding provided by Elastic DB
- Search in given time range
- HTTP endpoint for posting logs
- Ingestion Buffer & Batch processing
- Filters on specific fields
- Combination of all filters & search

### Built With

- Golang
- Python
- ElasticSearch
- Kafka
- Gin
- React


<!-- GETTING STARTED -->

## Getting Started

### Prerequisites

- Python 
- Node JS & npm
- Golang
- Docker (Other services can be installed directly or with Docker)

### Installation & usage

- Clone the repo

- Start the dependencies, you can use the docker-compose to setup:
  ```sh
  docker compose up -d
  ```
- You can check if all the services (ElasticSearch, Zookeeper, Kafka) are up and running by 
  ```sh
  docker ps
  ```

- Setup Log ingestion server

  1. Go to `log-server` directory
     ```sh
       cd log-server/
     ```
  2. Install golang dependencies
     ```sh
     go mod download
     ```
  3. Install Python dependencies
     ```sh
     pip install -r requirements.txt
     ```
  4. Start the ingestion server

     ```sh
     cd server
     GIN_MODE=release go run .
     ```

     The server should now be up and running on [http://localhost:3000](http://localhost:3000).

  5. This script is like a stress test, for a simultaneous bulk log insertion, the current value is 500, but can be modified as per requirements.
     Configure `LOGS_LENGTH` in `log-server/tests/performance_test.py`.

     ```sh
     python tests/performance_test.py
     ```

- Setup UI

  1. Go to `frontend` directory
     ```sh
       cd frontend/
     ```
  2. Install NPM dependencies
     ```sh
     npm install
     ```
  3. Start the React app
     ```sh
     npm start
     ```
  4. Frontend should be up at - [http://localhost:3006](http://localhost:3006)

- Simulate Log Publishers (logs via http endpoint)

  1.  Assuming all the services are up and running.

  3.  Start publisher script.
      Go to `log-producers` 
      ```sh
      cd log-server/log-producers
      ```
      Start a producer to simulate service using `--topic` option in different shells.
      Configured topics: `auth`,`database`,`email`,`payment`,`server`,`services`, for example
      ```sh
      python producer.py --topic payment
      python producer.py --topic auth
      ```
