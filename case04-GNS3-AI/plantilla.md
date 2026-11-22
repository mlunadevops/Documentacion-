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

**Create the working folder and enter it::**

```text
python3 -m venv csr1kv
```

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




