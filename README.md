# Ansible Playbook for Django Application Deployment

This repository contains an Ansible playbook to automate the deployment of a Django application with PostgreSQL and nginx on an Ubuntu 22.04 server.

## Prerequisites

- SSH access to the host machine.
- Ansible installed on your local machine.

## Setup

1. **Clone the Repository**

    ```bash
    git clone https://github.com/Husseinhassan1/Ansible-Playbook.git
    cd Ansible-Playbook
    ```

2. **Configure SSH Access**

    Ensure you have SSH access to the host machine. Update the `remote_user` variable in the `ansible.cfg` file with the user that will connect to the host.

    **File: `ansible.cfg`**

    ```ini
    [defaults]
    inventory = inventory.ini
    remote_user = <your_user>
    host_key_checking = False
    ```

3. **Set Host IP Address**

    Update the `ansible_host` variable in the `inventory.ini` file with the host IP address.

    **File: `inventory.ini`**

    ```ini
    [servers]
    app_server ansible_host= <your_host_ip_address>
    ```

4. **Update Variables**

    Update the `vars.yml` file with your user credentials.

    **File: `vars.yml`**

    ```yaml
    ---
    db_user: django_user
    db_password: your_secure_password
    db_name: django_db
    django_db_password: your_secure_password
    ```

## Running the Playbook

Execute the playbook to deploy the application:

```bash
ansible-playbook playbook.yml
```

## Verifying the Deployment

1. **Check the Django Application**

    - Navigate to `http://<your_host_ip_address>/healthcheck/`. You should see the health check status JSON.

2. **Check System Services**

    Ensure that the required services (nginx, PostgreSQL, Django) are running:

    ```bash
    sudo systemctl status nginx
    sudo systemctl status postgresql
    sudo systemctl status django
    ```

## File Structure

```plaintext
|-- ansible.cfg
|-- inventory.ini
|-- playbook.yml
|-- roles
|   |-- common
|   |   `-- tasks
|   |       `-- main.yml
|   |-- django
|   |   |-- handlers
|   |   |   `-- main.yml
|   |   |-- tasks
|   |   |   `-- main.yml
|   |   `-- templates
|   |       `-- django.service.j2
|   |-- nginx
|   |   |-- handlers
|   |   |   `-- main.yml
|   |   |-- tasks
|   |   |   `-- main.yml
|   |   `-- templates
|   |       `-- nginx.conf.j2
|   `-- postgresql
|       |-- handlers
|       |   `-- main.yml
|       |-- tasks
|       |   `-- main.yml
|       `-- templates
|           `-- pg_hba.conf.j2
`-- vars.yml
```
