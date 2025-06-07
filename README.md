# Roboshop Automation with Ansible Roles

This project automates the deployment and configuration of the Roboshop microservices application using Ansible roles. Roboshop is a cloud-native, multi-tier e-commerce application composed of several microservices such as catalogue, cart, user, payment, shipping, and frontend, each running as a separate service.

## Project Overview

The goal of this project is to provide a fully automated, repeatable, and modular way to set up the entire Roboshop stack on Linux servers. By leveraging Ansible roles, each microservice is managed independently, making the automation scalable, maintainable, and reusable.

### Key Features
- **Role-based Structure:** Each microservice (e.g., cart, catalogue, user, payment, shipping, frontend) has its own Ansible role, encapsulating all tasks, templates, files, and variables required for its setup.
- **Idempotent Playbooks:** Ensures that running the playbooks multiple times will not cause errors or duplicate changes.
- **Separation of Concerns:** Variables, handlers, templates, and files are organized per role, making the codebase clean and easy to manage.
- **Service Management:** Uses Ansible modules to manage systemd services, install packages, configure files, and handle application code deployment.

## Ansible Modules Used
- **ansible.builtin.dnf:** For installing and managing packages on RHEL-based systems.
- **ansible.builtin.command:** For running shell commands, such as enabling/disabling modules.
- **ansible.builtin.service:** For starting, stopping, enabling, and restarting systemd services.
- **ansible.builtin.file:** For managing files and directories (creating, deleting, setting permissions).
- **ansible.builtin.get_url:** For downloading application artifacts from remote sources.
- **ansible.builtin.unarchive:** For extracting application code from zip files.
- **ansible.builtin.template:** For deploying configuration files with Jinja2 templating, allowing dynamic variable substitution.
- **ansible.builtin.copy:** For copying static files to target hosts.
- **community.general.npm:** For installing Node.js dependencies in Node.js-based services.
- **ansible.builtin.user:** For creating and managing system users.
- **ansible.builtin.systemd_service:** For reloading systemd when new service files are deployed.

## Project Evolution

- **Initial Version:**
  - The Roboshop automation was originally implemented using a single, monolithic Ansible playbook. All tasks for all services were written in one file, making it harder to maintain and scale as the project grew.

- **Current Version (Role-based):**
  - The project was refactored to use Ansible roles. Each microservice now has its own role, with dedicated tasks, variables, templates, and handlers. This modular approach improves maintainability, reusability, and clarity. It also allows teams to work on different services independently and makes it easier to add or update services in the future.

## How It Works

1. **Inventory:**
   - The `roboshop.ini` inventory file defines all target hosts for each microservice.
2. **Playbooks:**
   - The main playbook (`main.yml`) dynamically applies the appropriate role to each host group.
3. **Roles:**
   - Each role contains:
     - `tasks/main.yml`: Step-by-step automation for the service.
     - `templates/`: Jinja2 templates for configuration files.
     - `files/`: Static files required by the service.
     - `vars/main.yml`: Role-specific variables.
     - `handlers/main.yml`: Handlers for service restarts and reloads.
4. **Execution:**
   - Run the playbook with Ansible, and it will provision, configure, and start all Roboshop services in the correct order.

## Benefits
- **Modular and Scalable:** Easily add new services or update existing ones.
- **Reusable:** Roles can be reused across different environments or projects.
- **Maintainable:** Clear separation of logic and configuration for each service.
- **Production-ready:** Ensures consistent, repeatable deployments.

---

> This project demonstrates best practices in Ansible automation for microservices and is a great starting point for anyone looking to automate complex, multi-tier applications.
