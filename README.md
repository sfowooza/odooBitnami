# Odoo Bitnami Installation

We will install Odoo 17 the bitnami odoo package on Ubuntu 

## Requirements

- Docker Installation:
  ```
  https://docs.docker.com/desktop/install/linux/ubuntu/
  ```
- Docker Compose
  ```
  https://phoenixnap.com/kb/install-docker-compose-on-ubuntu-20-04
  ```

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
9. check user is active and has permissions
    ```bash
    UPDATE res_users 
    SET active = true, share = false 
    WHERE login = 'user@example.com';
    ```
10 Set a temporary password

    ```bash
    UPDATE res_users 
    SET password = 'temppassword123'
    WHERE login = 'user@example.com';
    ```
## Usage

Go to the borwser and open odoo with the port you specified

```bash
localhost:80
