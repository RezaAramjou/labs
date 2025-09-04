# Cybersecurity Lab Environment Files

This repository contains miscellaneous files and configurations used to support the hands-on labs in my 30-day cybersecurity capstone project.

---

## ## Contents

* **`/docker`**: Contains Docker Compose files for quickly standing up containerized services.
* **`/pcaps`**: Contains sample network traffic captures for analysis.

---

## ## How to Use

### ### Running OWASP Juice Shop

The Juice Shop application is used as a target for penetration testing exercises.

1.  Ensure Docker and Docker Compose are installed.
2.  From the root of this repository, run the following command to start the container:
    ```bash
    docker-compose -f docker/juice-shop/docker-compose.yml up -d
    ```
3.  The application will be available at `http://localhost:3001`.

### ### Running LocalStack

LocalStack is used to simulate AWS services locally for cost-free Terraform testing.

1.  Ensure Docker and Docker Compose are installed.
2.  From the root of this repository, run the following command to start the container:
    ```bash
    docker-compose -f docker/localstack/docker-compose-localstack.yml up
    ```
3.  The LocalStack gateway will be available at `http://localhost:4566`.
