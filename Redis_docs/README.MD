# Redis Setup using Ansible Role

| **Author** | **Created on** | **Version** | **Last updated by**|**Internal Reviewer** |**Reviewer L0** |**Reviewer L1** |**Reviewer L2** |
|------------|---------------------------|-------------|---------------------|-------------|-------------|-------------|-------------|
| Anuj yadav|   12-02-2025             | v1.1          | Anuj yadav     |  Siddharth pawar | Tarun Singh  | Abhishek  | Abhishek Dubey|     
 

## Table of Contents
- [Introduction](#introduction)
- [Pre-requisites](#pre-requisites)
- [System Requirements](#system-requirements)
- [Dependencies](#dependencies)
- [Runtime Dependencies](#runtime-dependencies)
- [Important Ports](#important-ports)
- [Redis Overview](#redis-overview)
- [Key Features of Redis](#key-features-of-redis)
- [Important Configuration Files in Redis](#important-configuration-files-in-redis)
- [Install Redis](#install-redis)
- [Install Ansible](#install-ansible)
- [Flow Diagram](#flow-diagram)
- [Creating a Role](#creating-a-role)
- [Folder Structure](#folder-structure)
- [Variables](#variables)
- [Subtasks Files](#subtasks-files)
- [Templates for Configuration](#templates-for-configuration)
- [Run Playbook](#run-playbook)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)

## Introduction
This guide walks you through the steps needed to install and configure Redis using Ansible. It includes detailed instructions on pre-requisites, system requirements, dependencies, ports, and more.

## Pre-requisites
Before proceeding with the installation, ensure you have the following:

- A working Linux environment
- A user with sudo privileges
- Basic understanding of Ansible and Redis

## System Requirements
The following system requirements must be met:

| Requirement    | Minimum Specification |
|----------------|-----------------------|
| **RAM**        | 2GB or more           |
| **CPU Cores**  | 1 or more             |
| **Disk Space** | 10GB or more          |

## Dependencies

### Runtime Dependencies
Ensure you have the following software installed:

- Python 3.x
- Ansible

## Important Ports
Redis requires the following ports to be open:

| Port  | Description           |
|-------|-----------------------|
| 6379  | Redis server port     |

## Redis Overview
Redis is an open-source, in-memory data structure store that supports a variety of abstract data types, such as strings, hashes, lists, sets, and more. It is often used as a caching layer or session store.

## Key Features of Redis
- **In-memory storage:** Redis stores all data in memory for fast access.
- **Persistence options:** Redis provides various ways to persist data to disk.
- **High performance:** Redis is known for its high throughput and low latency.
- **Pub/Sub system:** Redis supports a publish/subscribe mechanism for real-time messaging.

## Important Configuration Files in Redis
- **redis.conf**: Main configuration file.
- **/etc/systemd/system/redis.service**: Service management configuration for Redis.

## Install Redis
To install Redis on your system, follow the [Redis installation guide](https://redis.io/docs/getting-started/).

## Install Ansible
To install Ansible on your system, follow the [Ansible installation guide](https://docs.ansible.com/ansible/latest/installation_guide/index.html).

## Flow Diagram
(Include flow diagram image here)

## Creating a Role
To create a new role in Ansible, you can use the `ansible-galaxy` command. This will generate the necessary folder structure for your role.

Run the following command to create a role for Redis setup:

```bash
ansible-galaxy init redis
```
## Folder Structure


## Variables
The following variables are used for configuring Redis installation:

| Variable        | Value        | Description                           |
|-----------------|--------------|---------------------------------------|
| `redis_version` | "6.2"        | Redis version to be installed.        |
| `redis_user`    | "redis"      | User for running Redis.               |
| `redis_group`   | "redis"      | Group for Redis user.                 |
| `redis_port`    | "6379"       | Redis server port.                    |
| `redis_bind`    | "127.0.0.1"  | Redis bind address.                   |

## Subtasks Files
These files are included in the `dependence.yml`, `redis_setup.yml`, and `redis.yml` playbooks.

- **dependence.yml**: This Ansible playbook updates the package cache, installs required packages (using a variable `required_packages`), and ensures that Redis' required services are running and enabled at boot.
- **redis_setup.yml**: This playbook ensures that Redis is installed, the configuration is updated, and the service is managed.
- **redis.yml**: This playbook handles all tasks related to Redis, including downloading and extracting Redis, creating the required user/group, configuring Redis, and setting up systemd services.

## Templates for Configuration
Two Jinja2 templates are required for configuring Redis:

- **redis.conf.j2**: This template includes parameters to configure Redis settings.
- **redis.service.j2**: This template creates a service file for setting up `redis.service` to manage Redis as a system service.

## Run Playbook
Once you have set up your environment and playbooks, you can run the Ansible playbook by executing the following command:

```bash
ansible-playbook -i <inventory-file> <playbook-name>
```
## Conclusion
Ansible Roles simplify infrastructure management by automating deployments, ensuring efficiency and consistency. This guide shows how to deploy Redis in a development environment using Ansible. Following these steps ensures Redis runs smoothly, scales with your needs, and reduces human error.

Ansible automates the entire Redis setup, making it ideal for both development and production environments.

## Contact Information
| Name        | Email Address                | GitHub Username | GitHub URL  |
|-------------|------------------------------|-----------------|-------------|
| Anuj Yadav  | anuj.yadav@mygurukulam.co     | anuj169         | [GitHub](https://github.com/anuj169) |

For more details or queries, reach out via email or visit the GitHub repository.

## Reference
- [Redis Installation Guide](https://redis.io/docs/getting-started/)
- [Ansible Installation Guide](https://docs.ansible.com/ansible/latest/installation_guide/index.html)
- [Redis Setup with Ansible](https://github.com/anuj169/redis-setup-ansible)
