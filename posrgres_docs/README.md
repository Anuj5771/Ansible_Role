# PostgreSQL Setup using Ansible Role

**Author**: Anuj Yadav  
**Created on**: 12-02-2025  
**Version**: 1.1  
**Last updated by**: Anuj Yadav  
**Internal Reviewer**: Siddharth Pawar  
**Reviewer L0**: Tarun Singh  
**Reviewer L1**: Abhishek  
**Reviewer L2**: Abhishek Dubey  

## Table of Contents
1. [Introduction](#introduction)
2. [Pre-requisites](#pre-requisites)
3. [System Requirements](#system-requirements)
4. [Dependencies](#dependencies)
    - [Runtime Dependencies](#runtime-dependencies)
5. [Important Ports](#important-ports)
6. [PostgreSQL Overview](#postgresql-overview)
7. [Key Features of PostgreSQL](#key-features-of-postgresql)
8. [Important Configuration Files in PostgreSQL](#important-configuration-files-in-postgresql)
9. [Install PostgreSQL](#install-postgresql)
10. [Install Ansible](#install-ansible)
11. [Flow Diagram](#flow-diagram)
12. [Creating a Role](#creating-a-role)
    - [Folder Structure](#folder-structure)
    - [Variables](#variables)
    - [Subtasks Files](#subtasks-files)
    - [Templates for Configuration](#templates-for-configuration)
13. [Run Playbook](#run-playbook)
14. [Conclusion](#conclusion)
15. [Contact Information](#contact-information)

---

## Introduction

This guide walks you through the steps needed to install and configure PostgreSQL using Ansible. It includes detailed instructions on pre-requisites, system requirements, dependencies, ports, and more.

---

## Pre-requisites

Before proceeding with the installation, ensure you have the following:

- A working Linux environment
- A user with sudo privileges
- Basic understanding of Ansible and PostgreSQL

---

## System Requirements

The following system requirements must be met:

| Requirement   | Minimum Specification |
| ------------- | --------------------- |
| **RAM**       | 2GB or more           |
| **CPU Cores** | 1 or more             |
| **Disk Space**| 10GB or more          |

---

## Dependencies

### Runtime Dependencies

Ensure you have the following software installed:

- **Python 3.x**
- **Ansible**

---

## Important Ports

PostgreSQL requires the following ports to be open:

| Port | Description |
| ---- | ----------- |
| 5432 | PostgreSQL server port |

---

## PostgreSQL Overview

PostgreSQL is a powerful, open-source relational database management system (RDBMS) that supports both SQL and NoSQL features. It is known for its extensibility, scalability, and compliance with SQL standards.

---

## Key Features of PostgreSQL

- **ACID-compliant**: PostgreSQL is fully compliant with the ACID (Atomicity, Consistency, Isolation, Durability) properties of database management.
- **Extensible**: You can define your own custom types, functions, and more.
- **Concurrency**: PostgreSQL uses Multi-Version Concurrency Control (MVCC) for handling multiple processes and high transaction rates.
- **Foreign keys, joins, views**: Supports advanced features like foreign keys, joins, views, stored procedures, and more.

---

## Important Configuration Files in PostgreSQL

- **postgresql.conf**: Main configuration file for PostgreSQL.
- **pg_hba.conf**: Configuration file for client authentication.
- **/etc/systemd/system/postgresql.service**: Service management configuration for PostgreSQL.

---

## Install PostgreSQL

To install PostgreSQL on your system, follow the [PostgreSQL installation guide](#).

---

## Install Ansible

To install Ansible on your system, follow the [Ansible installation guide](#).

---

## Flow Diagram

(Include flow diagram image here)

---

## Creating a Role

To create a new role in Ansible, you can use the `ansible-galaxy` command. This will generate the necessary folder structure for your role.

Run the following command to create a role for PostgreSQL setup:

```bash
ansible-galaxy init postgresql
```
## Folder Structure

The folder structure generated for the `postgresql` role will look like this:

```bash
postgresql/
├── defaults/
├── files/
├── handlers/
├── meta/
├── tasks/
├── templates/
└── vars/
# PostgreSQL Setup with Ansible

This repository contains Ansible playbooks and roles to automate the installation and configuration of PostgreSQL in a development environment. It simplifies the process of setting up PostgreSQL by automating common tasks, ensuring consistency and reducing human error.

## Variables

The following variables are used to configure the PostgreSQL installation:

| Variable            | Value       | Description                             |
|---------------------|-------------|-----------------------------------------|
| `postgres_version`   | `"13"`      | The version of PostgreSQL to install.   |
| `postgres_user`      | `"postgres"`| The user for running PostgreSQL.        |
| `postgres_group`     | `"postgres"`| The group for the PostgreSQL user.      |
| `postgres_port`      | `"5432"`    | The PostgreSQL server port.            |
| `postgres_bind`      | `"127.0.0.1"`| The PostgreSQL bind address.            |

## Playbooks

This repository contains the following playbooks:

### `dependence.yml`
- Updates the package cache.
- Installs required dependencies.
- Ensures that the PostgreSQL service is running and enabled at boot.

### `postgres_setup.yml`
- Installs PostgreSQL.
- Updates PostgreSQL configurations.
- Manages the PostgreSQL service.

### `postgres.yml`
- Downloads and extracts the PostgreSQL binaries.
- Creates the required PostgreSQL user and group.
- Configures PostgreSQL settings.
- Sets up systemd services for PostgreSQL.

## Templates for Configuration

### `postgresql.conf.j2`
This is a Jinja2 template used to configure PostgreSQL settings.

### `postgres.service.j2`
This is a Jinja2 template used to create a systemd service file (`postgresql.service`) to manage PostgreSQL as a service.

## Running the Playbook

Once you have set up your environment and playbooks, run the Ansible playbook with the following command:

```bash
ansible-playbook -i <inventory-file> <playbook-name>
```
## Conclusion

Ansible roles simplify infrastructure management by automating deployments, ensuring efficiency, and consistency. This guide demonstrates how to deploy PostgreSQL in a development environment using Ansible. Following these steps ensures PostgreSQL runs smoothly, scales with your needs, and reduces human error.

Ansible automates the entire PostgreSQL setup, making it ideal for both development and production environments.

## Contact Information

| Name       | Email Address                | GitHub Username | GitHub URL                  |
|------------|------------------------------|-----------------|-----------------------------|
| Anuj Yadav | anuj.yadav@mygurukulam.co     | anuj169         | [GitHub](https://github.com/anuj169) |

For more details or queries, feel free to reach out via email or visit the GitHub repository.

## References

- [PostgreSQL Installation Guide](https://www.postgresql.org/docs/)
- [Ansible Installation Guide](https://docs.ansible.com/)
- [PostgreSQL Setup with Ansible](https://github.com/anuj169/PostgreSQL-Ansible-Setup)

