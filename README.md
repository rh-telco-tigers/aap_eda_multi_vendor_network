# Ansible Event-Driven Multi-Vendor Network Automation

This repository contains an Ansible event-driven framework for automating network configurations across multiple vendor devices. The solution leverages Ansible’s extensible nature to provide a standardized way to automate network tasks, respond to events, and manage diverse network infrastructure.

## Overview

This project enables network engineers to manage multi-vendor network devices using event-driven automation. By defining events, triggers, and actions, the framework allows for responsive and automated network operations such as configuration changes, monitoring, and alerting.
Features

    Event-Driven Automation: Execute specific tasks based on defined events and triggers.
    Multi-Vendor Support: Manage devices from various vendors using a unified Ansible playbook structure.
    Modular and Extensible: Easily extend support for additional vendors and network features.
    Logging and Alerting: Built-in support for logging actions and alerting based on event outcomes.
    Scalability: Suitable for small to large network environments.

![Alt text](https://github.com/rh-telco-tigers/aap_eda_multi_vendor_network/blob/6b78b179a6966847c9016d8340acf4cc7f7c5ec8/Multi-Vendor%20Event%20Driven%20Ansible.png)

## Prerequisites

Ensure the following software is installed and configured:

    Ansible >= 2.9
    Python >= 3.6
    Network device credentials stored securely (e.g., Ansible Vault, environment variables)
    Ansible collections for each supported vendor (e.g., cisco.ios, arista.eos, junipernetworks.junos)
    AAP Environment with Ansible Automation Controller, Ansible Private Automation Hub and Ansible Event Driven Controller.
    Openconfig installed on network devices.
