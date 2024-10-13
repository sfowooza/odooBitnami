
# Odoo Bitnami Installation

We will install Odoo 17 the bitnami odoo package on Ubuntu 

## Requirements
- Text Editor - Vim , VS Code etc

- Docker Installation:Refer to tutorial below
  
  [Docker Installtion](https://docs.docker.com/desktop/install/linux/ubuntu/)
  
- Docker Compose: Refer to Tutorial below

  [Docker Compose Installation](https://phoenixnap.com/kb/install-docker-compose-on-ubuntu-20-04)
  
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
4. Create a custom addons folder in host:
    ```bash
    mkdir -p odoo/custom_addons
    ```
5. Update the docker-compose.yml file for the host custom_addons to point to container addons folder
    ```bash
        volumes:
      - 'odoo_data:/bitnami/odoo'
      - '/Odoo17Bitnami/odoo/custom_addons:/opt/bitnami/odoo/custom_addons'
    ```
6. Create/Update the Docker-compose YAML file inside Odoo17Bitnami:
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
          - '/home/sendowooza/Desktop/Odoo17Bitnami/odoo/custom_addons:/opt/bitnami/odoo/custom_addons'
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
7. Update the odoo port to your desired
   ```bash
   - '78:8069'
   ```
9. Start Odoo docker compose :
    ```bash
   docker-compose up -d
    ```
10. Docker will automatically pull odoo bitnami package and create the odoo and odoo postgres container as shown below
    ![docker4](https://github.com/user-attachments/assets/0448be54-6fa1-4be3-84a0-9e00184a4dac)
    Confirm the the odoo containers are up and running
    ```bash
    docker ps -a
    ```
    ![docker6](https://github.com/user-attachments/assets/019a4d92-8407-47fd-b01a-249c2efdc734)

    ```
## Usage

Go to the borwser and open odoo with the port you specified

```bash
localhost:78
```
As shown below

![odoo1](https://github.com/user-attachments/assets/55004fa4-b100-471d-a24a-ccc97ba475df)

After installing Odoo 17 using the Bitnami Docker image and running the container, you can typically access the Odoo web interface using the following default credentials:
```bash
Email: user@example.com
Password: bitnami
```
However, it's important to note that these are default credentials, and for security reasons, you should change them immediately after your first login.

11. Enter your Odoo container to update user preferences
    ```bash
    docker exec --user root -it [YOUR ODOO CONTAINER] /bin/bash
    ```
    Replace YOUR ODOO CONTAINER with your Docker odoo container Example : mine is "odoo17bitnami-odoo-1"
12. Once inside the odoo container install necessary packages :
    ```bash
    apt-get update
    ```
    And
    ```
    apt install wget vim zip unzip
    ```
    As indicated below
    ![odoo_container1](https://github.com/user-attachments/assets/197b1a0f-ac42-4d26-9805-9a0ba06fa0f5)

    OPTIONALLY: You Can access the Odoo container files through VS Code Docker route as shown below
    
    ![container2](https://github.com/user-attachments/assets/31b7a07e-dfa3-4678-a65c-e92f461dad62)
13. Update your odoo configuration file odoo.conf as shown above with your preferred user password and also your host custom addons path :
    ```bash
    addons_path = /opt/bitnami/odoo/addons /opt/bitnami/odoo/custom_addons
    admin_passwd = [Your-set-password]
    ```
14. Go to your Postgres Container as in Step 11 and login into the database: bitnami_odoo with user: bn_odoo with the belwo command
    ```
    psql -U bn_odoo -d bitnami_odoo
    ```
15. To list database roles (users):
    ```
    \du
    ```
    This shows roles and their attributes, but not emails or passwords.
    To list users with their login (which is often an email in Odoo):
    ```
    SELECT id, login, active FROM res_users;
    ```
17. check user is active and has permissions
    ```bash
    UPDATE res_users 
    SET active = true, share = false 
    WHERE login = 'user@example.com';
    ```
18. You can update and change to your custom login email
    ```
    UPDATE res_users 
    SET login = 'fssendowooza@gmail.com'
    WHERE login = 'user@example.com';
    ```
20. Set a temporary password

    ```bash
    UPDATE res_users 
    SET password = 'temppassword123'
    WHERE login = 'fssendowooza@gmail.com';

    
![odooscre](https://github.com/user-attachments/assets/4ca5801a-3658-4d95-8b30-ec5ed5b7b3f9)

21. Download and install custom modules in the custom-addons folder
    Custom open source modules can be obtained from the Odoo Apps official site (Link Below) be sure to filter category, Version etc
    [Oddo module App store](https://apps.odoo.com/apps)
    
    Or from the Odoo Community Association (OCA) github handle on the link below
    [OCA Github modules](https://github.com/oca)
