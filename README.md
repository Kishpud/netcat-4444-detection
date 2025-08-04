# Netcat 4444 Detection – SOC Home Lab Project

This project simulates and detects a **reverse shell connection** using Netcat on port `4444`, and showcases how to monitor it using **Zeek**, **Filebeat**, and the **ELK Stack** (Elasticsearch + Kibana).  
It demonstrates real-world SOC detection skills useful in identifying unauthorized remote access attempts.

---

## 🔍 Project Purpose

- Simulate a **reverse shell attack** from a Windows host to an Ubuntu SOC machine.
- Capture and log the activity using **Zeek**.
- Parse and ship logs via **Filebeat** to **Elasticsearch**.
- Visualize suspicious connections in **Kibana**.

---

## 🧪 Tools Used

| Tool         | Purpose                                      |
|--------------|----------------------------------------------|
| Netcat (nc)  | To simulate reverse shell                     |
| Zeek         | To capture and log network traffic            |
| Filebeat     | To forward logs from Zeek to Elasticsearch    |
| Elasticsearch| To store structured logs                     |
| Kibana       | To visualize alerts and traffic patterns      |

---

## ⚙️ Simulation Steps

1. **Start Netcat listener** on Ubuntu:
    ```bash
    nc -lvnp 4444
    ```

2. **Connect from Windows attacker machine:**
    ```cmd
    nc64.exe <Ubuntu_IP> 4444
    ```

3. **Exchange sample message:**
    ```
    hey bud m windows
    ```

4. **Verify Zeek logs:**
    ```bash
    cat /usr/local/zeek/logs/current/conn.log | grep 4444
    ```

5. **Query via Elasticsearch:**
    ```bash
    curl -X GET "localhost:9200/filebeat-*/_search?q=dest_port:4444&pretty"
    ```

6. **Visualize in Kibana:**
    - Vertical bar graph showing destination IPs and connection states (e.g., SF, REJ)

---

## 📸 Screenshots

### Windows Machine (Reverse Shell Trigger)
<img src="Screenshot 2025-08-05 at 8.13.24 am.png" width="700"/>

---

### Zeek Logs Showing Port 4444 Activity
Screenshot from 2025-08-04 22-07-20.png 

---

### Elastic/Kibana Dashboards

Screenshot from 2025-08-04 22-23-06.png
---

## 📈 Why This Matters (Blue Team Relevance)

- **SOC Analysts** must detect unusual port usage like 4444 (commonly used in reverse shells).
- Helps build **threat detection** logic using logs.
- Encourages **real-world skills**: log parsing, alerting, visualization, and correlation.
- Prepares for detecting **C2 channels**, **brute force**, and **lateral movement** patterns.

---

## 👨‍💻 Author

- **Name:** Kishor Pudasaini (Kisu)  
- **Location:** Sydney, Australia  
- **Focus:** SOC Analyst | Cybersecurity | Threat Detection

---

> _This project is part of my self-built SOC home lab. All attack traffic is generated in a safe, controlled environment for learning purposes only._
