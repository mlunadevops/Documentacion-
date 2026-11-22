# TECHNICAL LOG & BGP ENGINEERING GUIDE

## Automated Testing Using pyATS and Genie
**CCNP Miguelangel Luna**

---

## CONTENIDOS:

| Case | Title | Description |
| :--- | :--- | :--- |
| **01** | [Claude & n8n AI Agents](./case-01-Google-Auth/) | Agentes Claude . |

[Google](https://www.google.com)

## 1. Introduction and Theoretical Framework

Objectives:

**Parts 1 and 2:** Create a Python virtual environment (venv).

**Part 3:** Install and use the pyATS testing library.

**Part 4:** Use Genie to parse IOS command output into JSON.

**Part 5:** Use Genie to compare configurations.

**Part 6:** Cleanup and exploration.

## 2. Topology and BGP Neighbor Establishment

The

![BGP WEIGTH](images/01Topologia.jpg)


## 3. IMPLEMENTATION:

**Parts 1 and 2:** Create a Python virtual environment (venv).
We are going to create an "isolated space" to install pyATS without affecting the VM's base system.

**1.1) Create the working folder and enter it::**

```text
python3 -m venv csr1kv
```

What does each part mean?

**python3:** Runs the Python 3 interpreter on your system.

**-m venv:** Tells Python to run the venv module (included by default in Python 3.3+) as a script to create virtual environments.

**csr1kv:** This is the name (and the folder) that will be given to the virtual environment. In this case, it is usually used as a folder or project name related to the Cisco CSR 1000v virtual router (for example, for network automation scripts with Netmiko, NAPALM, Ansible, or pyATS).


**Enter the virtual environment:**

```text
cd csr1kv
source bin/activate
```

**Part 3:** Use the pyATS Testing Library

Step 1: Install pyATS
Inside the virtual environment (make sure you see (csr1kv) in your terminal), run:

```text
pip3 install pyats[full]
```

(This command will download quite a few packages. It may take a few minutes. If you see some compilation errors along the way, they can usually be ignored as long as the installation finishes.)


### 4. BGP Configuration:




