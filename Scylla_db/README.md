# ScyllaDB Setup using Ansible Role

![image](https://github.com/user-attachments/assets/f962e877-2a78-455a-b75f-acd5485683d5)

| **Author** | **Created on** | **Version** | **Last updated by**|**Internal Reviewer** |**Reviewer L0** |**Reviewer L1** |**Reviewer L2** |
|------------|---------------------------|-------------|---------------------|-------------|-------------|-------------|-------------|
| Anuj yadav|   12-02-2025             | v1.1          | Anuj yadav     |  Siddharth pawar | Tarun Singh  | Abhishek  | Abhishek Dubey|     

## Table of Contents
1. [Introduction](#introduction)  
2. [Pre-requisites](#pre-requisites)  
3. [System Requirements](#system-requirements)  
4. [Dependencies](#dependencies)  
    - [Runtime Dependencies](#runtime-dependencies)  
5. [Important Ports](#important-ports)  
6. [ScyllaDB Overview](#scylladb-overview)  
7. [Key Features of ScyllaDB](#key-features-of-scylladb)  
8. [Important Configuration Files in ScyllaDB](#important-configuration-files-in-scylladb)  
9. [Install ScyllaDB](#install-scylladb)  
10. [Install Ansible](#install-ansible)  
11. [Flow Diagram](#flow-diagram)  
12. [Creating a Role](#creating-a-role)  
13. [Folder Structure](#folder-structure)  
14. [Variables](#variables)  
15. [Subtask Files](#subtask-files)  
16. [Templates for Configuration](#templates-for-configuration)  
17. [Run Playbook](#run-playbook)  
18. [Conclusion](#conclusion)  
19. [Contact Information](#contact-information)  

---


## Introduction
This guide walks you through the steps needed to install and configure ScyllaDB using Ansible. It includes detailed instructions on pre-requisites, system requirements, dependencies, ports, and much more.

## Pre-requisites
Before proceeding with the installation, ensure you have the following:
- A working Linux environment
- A user with sudo privileges
- Basic understanding of Ansible and ScyllaDB

## System Requirements

The following system requirements must be met:

| Requirement                | Minimum Specification      |
|----------------------------|----------------------------|
| **RAM**                    | 4GB or more                |
| **CPU Cores**              | 2 or more                  |
| **Disk Space**             | 10GB or more               |

## Dependencies

### Runtime Dependencies
Ensure you have the following software installed:
- Python 3.x
- Ansible

## Important Ports

ScyllaDB requires the following ports to be open:

| Port  | Description                             |
|-------|-----------------------------------------|
| **9042** | CQL (Cassandra Query Language) interface |
| **7000** | Cluster communication (internal)       |
| **7001** | Secure cluster communication           |
| **7199** | JMX monitoring                         |
| **9043** | Secure CQL (Cassandra Query Language) interface |

## ScyllaDB Overview
ScyllaDB is a high-performance NoSQL database designed to provide scalable, low-latency storage and retrieval of large amounts of data.

## Key Features of ScyllaDB
- **Low Latency**: Optimized for low-latency operations.
- **High Throughput**: Handles massive throughput with ease.
- **Auto Scaling**: Dynamically scales based on load.

## Important Configuration Files in ScyllaDB
- **scylla.yaml**: Main configuration file
- **cassandra-env.sh**: Environment configuration
- **scylla.conf**: Additional configuration options for ScyllaDB


```bash
# Authenticator and Authorizer settings
cassandra.authenticator=PasswordAuthenticator
cassandra.authorizer=CassandraAuthorizer

# List of seed nodes in the cluster (comma-separated list)
cassandra.seeds=172.31.30.107, 172.31.30.108

# Address to listen for remote procedure calls (RPC)
cassandra.rpc_address=172.31.30.107

# Specify the listen address for node-to-node communication
cassandra.listen_address=172.31.30.107

```

## Install Scylldb

To install SonarQube on your system, please follow the link below for the ScyllaDb Installation Guide:  
[SonarQube Installation Guide](https://github.com/snaatak-Zero-Downtime-Crew/Documentation/tree/main/Common/Software/ScyllaDB)

## Install Ansible

To install Ansible on your system, please follow the link below for the Ansible Installation Guide:  
[Ansible Installation Guide](https://github.com/snaatak-Zero-Downtime-Crew/Documentation/tree/main/Common/Software/Ansible/Installation)


## Flow Diagram

![image](https://github.com/user-attachments/assets/924f9c81-ac7a-4f05-a704-77f89472a87f)

## Creating a Role

To create a new role in Ansible, you can use the `ansible-galaxy` command. This will generate the necessary folder structure for your role.

Run the following command to create a role for SonarQube setup:

```bash
ansible-galaxy init scylladb
```
## Folder Structure

![image](https://github.com/user-attachments/assets/26dee18e-2553-4edd-a591-026bdd7d048e)

## Variables
The following variables are used for configuring ScyllaDB installation:

| **Variable**              | **Value**                     | **Description**                                                       |
|---------------------------|-------------------------------|-----------------------------------------------------------------------|
| **scylla_version**         | "4.6"                          | ScyllaDB version to be installed.                                     |
| **jdk_version**            | "17"                           | Java Development Kit version required for ScyllaDB.                   |
| **scylla_user**            | "scylla"                       | User for running ScyllaDB.                                            |
| **scylla_group**           | "scylla"                       | Group for ScyllaDB user.                                              |
| **scylla_db**              | "scylladb"                     | Database name for ScyllaDB.                                           |
| **scylla_db_user**         | "scylla_user"                  | Database user for ScyllaDB.                                           |
| **scylla_db_password**     | "scylla_password"              | Password for the ScyllaDB database user.                              |
| **scylla_web_port**        | "9042"                         | ScyllaDB web interface port.                                          |

## Subtasks Files

These files are included in the `dependence.yml`, `dboperation.yml`, and `scylladb.yml` playbooks.

- **dependence.yml**: This Ansible playbook updates the package cache, installs required packages (using a variable `required_packages`), and ensures that ScyllaDB's required services are running and enabled at boot.
  
- **dboperation.yml**: This Ansible playbook ensures that a ScyllaDB user and database exist. It creates the user if not present, updates the password, creates the database if missing, and grants full privileges to the user.

- **scylladb.yml**: This Ansible playbook installs and configures ScyllaDB by downloading and extracting it, creating a dedicated user and group, setting permissions, configuring ScyllaDB using templates, setting up a systemd service, and updating sysctl settings.

## Templates for Configuration

Two Jinja2 templates are required for configuring ScyllaDB:

- **scylladb.conf.j2**: This template includes parameters to configure the ScyllaDB database and its settings.
  
- **scylladb.service.j2**: This template creates a service file for setting up `scylladb.service` to manage ScyllaDB as a system service.

## Run Playbook

Once you have set up your environment and playbooks, you can run the Ansible playbook by executing the following command:

```bash
ansible-playbook -i <inventory-file> <playbook-name>
```
## Conclusion

Ansible Roles offer a modular approach to automate infrastructure management, making deployments efficient, consistent, and less error-prone. This guide illustrates the process of deploying ScyllaDB in a development environment through Ansible. By following these instructions, you can effectively provision and set up ScyllaDB, ensuring that your NoSQL database runs smoothly and scales according to your requirements.

With Ansible, the entire process of setting up ScyllaDB, from installation to configuration and service management, is automated, saving time and reducing human error. By using these guidelines, you can quickly deploy ScyllaDB in a reliable and repeatable manner, making it ideal for both development and production environments.

## Contact

| **Name**      | **Email Address**                  | **GitHub**                             | **URL**                                |
|---------------|------------------------------------|----------------------------------------|----------------------------------------|
| Anuj Yadav    | anuj.yadav@mygurukulam.co          | [anuj169](https://github.com/anuj169)  | [https://github.com/anuj169](https://github.com/anuj169) |

For more details or queries, feel free to reach out via email or visit the GitHub repository linked above.

## Reference

| **Resource**                      | **Link**                                                                         |
|------------------------------------|----------------------------------------------------------------------------------|
| **ScyllaDB Installation Guide**    | [ScyllaDB Installation Guide](https://docs.scylladb.com/getting-started/)         |
| **ScyllaDB Documentation**         | [ScyllaDB Documentation](https://docs.scylladb.com/)                             |
| **Ansible Installation Guide**     | [Ansible Installation Guide](https://docs.ansible.com/ansible/latest/installation_guide/index.html) |
| **ScyllaDB Setup with Ansible**    | [ScyllaDB Setup with Ansible](https://docs.scylladb.com/operating-scylla/ansible/) |

