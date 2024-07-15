# Odoo Bitnami Installation

We will install Odoo 17 the bitnami odoo package on Ubuntu 

## Requirements

- Docker Installation
- Dockaer Compose

## Installation

To install this project, follow these steps:

1. Clone the repository:
    ```bash
    git clone https://github.com/sfowooza/github.com/odooBitnami.git
    ```
2. Navigate to the project directory:
    ```bash
    mkdir Odoo17 
    ```
3. Enter into project:
    ```bash
    cd Odoo17
    ```
4. Create Docker-compose YAML file inside Odoo17:
    ```bash
    vim docker-compose.yml
    ```
5. Create a custom addons folder in host:
    ```bash
    mkdir -p odoo/custom_addons
    ```
6. Update the docker-compose.yml file for the host custom_addons to point to container addons folder
    ```bash
        volumes:
      - 'odoo_data:/bitnami/odoo'
      - '/OdooBit/odoo/custom_addons:/opt/bitnami/odoo/custom_addons'
    ```
7. Start Odoo docker compose :
    ```bash
   docker-compose up -d
    ```
8. Create a custom addons folder in host:
    ```bash
    mkdir -p odoo/custom_addons
    ```
## Usage

Go to the borwser and open odoo with the port you specified

```bash
localhost:80
