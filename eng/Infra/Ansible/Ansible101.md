# Ansible Basics

> Let's learn about Ansible
>
> Reference: [brownbears.tistory.com](https://brownbears.tistory.com/358)

<br>

<br>

## What is Ansible?

- An automation management tool that aims for **IaC (Infrastructure as Code)**
- Built on an Open-source basis
- The modules and libraries that run Ansible are Python-based
- Executes **playbooks** based on YAML format to
  1. Implement desired automation, or
  2. Run modules in Ad hoc mode to query the status
- Configures and manages automation on **Target Hosts** in an **agentless** manner based on **SSH**

<br>

<br>

## Advantages of Ansible

<br>

### 1. Agentless

- While most IaC tools generally use a **pull** method based on **agents** installed on target machines,
  - Ansible operates in a **push** method based on **agentless** approach on target machines
- Since no **agent** is installed on target machines, Data center or IT Infra administrators have relatively less resistance to adoption
- Since it mostly operates based on **SSH**, technical **accessibility** is also easy

<br>

### 2. Ease of Access

- Although Ansible is developed based on Python, the entry barrier is low enough to use without knowledge of Python

<br>

### 3. Diverse Module Support

- Versions are continuously patched, and with a broad user base, many modules are supported
- A very wide range of modules covering various cloud infra, virtualization, server OS, platforms, network equipment, and storage are expanded with each version upgrade

<br>

### 4. Idempotence

- In Ansible, even if you run a **Playbook** written as a YAML script file multiple times, it produces the same result, consistently achieving `idempotence`
  - The result does not change even if applied multiple times
    - If nothing has changed, it naturally remains unchanged even after deployment
    - If there are changes, only those parts are applied
  - Shell, command, and file modules are not guaranteed
- When Ansible runs, it first checks the module's state before performing a Task,
  - and even when performing a Task, it provides information about what has been added and changed, delivering **consistent** results

<br>

<br>

## Ansible Architecture

<br>

![ansible-architecture](../../kor/images/ansible-architecture.png)

### Control Node

- The central control node where Ansible is installed
  - Cannot be installed on Windows, so `winrm` must be used

<br>

### Managed Node

- A server managed by the Ansible **Control Node**
  - A target registered in **hosts**
- The Ansible **Control Node** deploys to **Managed Nodes** via **SSH**

<br>

### Inventory

- A list where **Managed Nodes** are registered
  - A file that contains connection information for nodes or servers to work with
  - A file that describes metadata about remote servers
- It can either read the default file `/etc/ansible/hosts` or you can create a separate **Inventory** file and run it with options
  - If there is a server with a static IP that is not in the **hosts** file, you can create a configuration file, which is useful when setting up test environments

<br>

### Modules

- Individual units of work executed in Ansible
- Helps easily perform tasks such as:
  - Package and service installation
  - File permission settings
  - Database operations
  - Cloud operations
  - Network operations

<br>

### Tasks

- A collection of Modules
- Unit of work

<br>

### Playbooks

- YAML files written to execute planned tasks in order
