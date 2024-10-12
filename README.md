# Odoo Bitnami Installation

We will install Odoo 17 the bitnami odoo package on Ubuntu 

## Requirements
- Text Editor - Vim , VS Code etc

- Docker Installation:
  
  [Docker Installtion](https://docs.docker.com/desktop/install/linux/ubuntu/)
  
- Docker Compose

  [Docker Compose Installation] (https://phoenixnap.com/kb/install-docker-compose-on-ubuntu-20-04)
  
  ![docker1](https://github.com/user-attachments/assets/d6b5186b-79f2-4f58-90c7-1fd7de5ee56f)


## Installation

To install this project, follow these steps:


1. Navigate to the project directory:
    ```bash
    mkdir Odoo17Bitnami
    ```
2. Enter into project:
    ```bash
    cd Odoo17Bitnami
    ```
3. Clone the repository:
    ```bash
    git clone https://github.com/bitnami/containers/blob/main/bitnami/odoo/docker-compose.yml
    ```
4. Create/Update the Docker-compose YAML file inside Odoo17Bitnami:
    ```bash
    vim docker-compose.yml
    ```
    #### Or Copy paste this below docker-compose.yml
   ```bash
    version: '3.8'
    services:
      postgresql:
        image: docker.io/bitnami/postgresql:17
        volumes:
          - 'postgresql_data:/bitnami/postgresql'
        environment:
          # ALLOW_EMPTY_PASSWORD is recommended only for development.
          - ALLOW_EMPTY_PASSWORD=yes
          - POSTGRESQL_USERNAME=bn_odoo
          - POSTGRESQL_DATABASE=bitnami_odoo
      odoo:
        image: docker.io/bitnami/odoo:17
        ports:
          - '78:8069'
        volumes:
          - 'odoo_data:/bitnami/odoo'
          - '/home/sendowooza/Desktop/Odoo16Bitnami/odoo/custom_addons:/opt/bitnami/odoo/custom_addons'
        depends_on:
          - postgresql
        environment:
          # ALLOW_EMPTY_PASSWORD is recommended only for development.
          - ALLOW_EMPTY_PASSWORD=yes
          - ODOO_DATABASE_HOST=postgresql
          - ODOO_DATABASE_PORT_NUMBER=5432
          - ODOO_DATABASE_USER=bn_odoo
          - ODOO_DATABASE_NAME=bitnami_odoo
    volumes:
      postgresql_data:
        driver: local
      odoo_data:
        driver: local
    ```
   
5. Create a custom addons folder in host:
    ```bash
    mkdir -p odoo/custom_addons
    ```
6. Update the docker-compose.yml file for the host custom_addons to point to container addons folder
    ```bash
        volumes:
      - 'odoo_data:/bitnami/odoo'
      - '/Odoo17Bitnami/odoo/custom_addons:/opt/bitnami/odoo/custom_addons'
    ```
7. Update the odoo port to your desired
   ```bash
   - '78:8069'
   ```
9. Start Odoo docker compose :
    ```bash
   docker-compose up -d
    ```
10. Create a custom addons folder in host:
    ```bash
    mkdir -p odoo/custom_addons
    ```
11. check user is active and has permissions
    ```bash
    UPDATE res_users 
    SET active = true, share = false 
    WHERE login = 'user@example.com';
    ```
12. Set a temporary password

    ```bash
    UPDATE res_users 
    SET password = 'temppassword123'
    WHERE login = 'user@example.com';
    ```
## Usage

Go to the borwser and open odoo with the port you specified

```bash
localhost:80
