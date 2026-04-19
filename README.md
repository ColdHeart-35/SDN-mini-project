# SDN-mini-project

# 🔥 Stateful Firewall using Ryu Controller (SDN)

## 📌 Overview

This project implements a **Stateful Firewall** using the **Ryu SDN Controller** and **Mininet**.
The controller inspects network traffic in real-time and applies rules to **allow, block, and track flows** between hosts.

Unlike a stateless firewall, this system **remembers previous connections** and allows **reply packets** automatically.

---

## 🚀 Features

* ✅ Real-time packet inspection using OpenFlow
* ❌ Blocking specific traffic (e.g., h1 → h2)
* 🔁 Stateful behavior (reply packets are allowed)
* 📊 Continuous logging of network activity
* 🌐 Works with Mininet virtual topology
* ⚡ No flow installation (ensures logging for every packet)

---

## 🏗️ System Architecture

```
+--------+       +-----------+       +--------+
|  Host1 | <---> |  Switch   | <---> |  Host2 |
+--------+       +-----------+       +--------+
                       |
                       ↓
                +-------------+
                | Ryu Controller |
                +-------------+
```

* **Switch (OVS)** forwards packets to controller
* **Ryu Controller** decides:

  * ALLOW ✅
  * BLOCK ❌
  * REPLY 🔁
* Decision is logged and applied instantly

---

## ⚙️ Technologies Used

* 🐍 Python
* 🌐 Ryu SDN Framework
* 🧪 Mininet
* 🔌 OpenFlow 1.3
* 🖧 Open vSwitch (OVS)

---

## 📂 Project Structure

```
ryu_project/
│── my_controller.py     # Firewall logic
│── README.md           # Documentation
│── ryu-env/            # Virtual environment (optional)
```

---

## 🧠 Firewall Logic

### 🔴 Block Rule

```
10.0.0.1 → 10.0.0.2  → BLOCKED
```

### 🟢 Allow Rule

```
10.0.0.2 → 10.0.0.1  → ALLOWED
```

### 🔁 Stateful Rule

```
Reply traffic → automatically ALLOWED
```

---

## 🛠️ Setup Instructions

### 1️⃣ Clean Environment

```bash
sudo mn -c
pkill -f ryu
```

---

### 2️⃣ Start Ryu Controller

```bash
cd ~/Documents/Pes4Sem/ryu_project
source ryu-env/bin/activate

ryu-manager --verbose my_controller.py
```

---

### 3️⃣ Start Mininet

```bash
sudo mn --controller=remote,ip=127.0.0.1,port=6653 \
        --topo single,3 \
        --switch ovsk,protocols=OpenFlow13
```

---

### 4️⃣ Test Connectivity

```bash
h1 ping h2
h2 ping h1
```

---

## 📊 Sample Output (Ryu Logs)

```
📦 Packet: 10.0.0.1 → 10.0.0.2
❌ BLOCKED

📦 Packet: 10.0.0.2 → 10.0.0.1
✅ ALLOWED

📦 Packet: 10.0.0.2 → 10.0.0.1
🔁 REPLY ALLOWED
```

---

## 🔍 Key Concepts Used

* OpenFlow Packet-In handling
* MAC learning switch logic
* Stateful firewall tracking
* Controller-based packet forwarding
* Real-time logging

---

## ⚠️ Important Notes

* Start **Ryu BEFORE Mininet**
* Do NOT restart controller while Mininet is running
* Ensure controller is connected:

```bash
ovs-vsctl show
```

---

## 🎯 Applications

* Network Security Testing
* SDN-based Firewalls
* Traffic Monitoring Systems
* Academic Research in SDN

---

## 📌 Conclusion

This project demonstrates how **Software Defined Networking (SDN)** enables flexible and programmable network security.
By using Ryu, we implemented a **stateful firewall** capable of making intelligent traffic decisions in real time.

---
