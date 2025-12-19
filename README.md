# Log-Analysis-Lab
🔐 SOC Analyst Log Analysis Lab

This repository contains a synthetic multi-source log file and supporting notes created to simulate real-world SOC analyst investigations across multiple layers of an environment (auth, web, endpoint, network, cloud, and database).
The goal of this project is to practice structured log analysis, detection engineering, and incident investigation workflows using a modern log management tool (such as Loggly).

---

🎯 Objectives

This project is designed to help build a SOC analyst mindset by focusing on:
1. Understanding how different attack techniques appear in logs.
2. Correlating events across multiple log sources.
3. Designing practical search queries and detection ideas.
4. Documenting findings in a clear, professional way.

---

📁 Dataset Overview

The main log file (JSON Lines format) includes realistic events for the following scenarios:

1. SSH brute-force attacks
    Multiple failed SSH login attempts targeting root from a single external IP, culminating in a detection event and automated blocking.

2. Web reconnaissance & SQL injection attempts
    Web server logs showing scanning (Nikto-style user agents, sensitive paths like /.env, phpinfo.php) followed by a WAF alert blocking a SQL injection payload.

3. Password spray activity
    Identity provider logs raising a password_spray_suspected event where many different user accounts are targeted from one IP over a short time window.

4. Impossible travel login
    A user successfully authenticates from one country and then appears to log in from a distant country within one minute, suggesting potential session/token compromise.

5. Malware indicators and C2 communication
    Endpoint logs capturing suspicious encoded PowerShell execution, plus DNS and firewall events showing queries to a lookalike domain and outbound C2-style connections.

6. Cloud privilege escalation (AWS-like IAM)
    Cloud audit logs showing a temporary user attaching AdministratorAccess to another account without MFA, representing a high-risk configuration change.

7. Database exfiltration attempts
    Database logs with a UNION_SELECT fingerprint, an unusually large number of rows returned, and elevated query duration, suggesting possible data extraction.

8. Log tampering and cover tracks
    Privilege escalation via sudo, creation of a new privileged account, followed by truncation of /var/log/auth.log to erase evidence.

---

🧪 How This Lab Will Be Used
Planned activities with this dataset:

1. Ingest into a log management platform
    Upload the JSONL file into a log platform (e.g., Loggly) as a single source.
    Verify that fields such as log_type, event, user, src_ip, and severity are parsed correctly.

2. Design and test search queries

    Build queries for:
      Password spray detection
      Malware/encoded PowerShell execution
      Suspicious database activity
      Log tampering and privilege escalation
    Iterate on filters and field-based searches to reduce noise and increase signal.

3. Correlation and investigation workflows
     Pivot from a single suspicious host (e.g., workstation or server) to all related events.
     Connect endpoint events to network, identity, and cloud activity.
     Reconstruct a timeline of attacker behavior across the entire environment.

4. Detection & alert ideas

    Define basic detection rules based on this dataset:
      Threshold-based rules (e.g., failed logins per IP / user).
      Pattern-based rules (e.g., -enc PowerShell commands, UNION_SELECT).
      Behavioral rules (e.g., impossible travel, log clearing after privilege escalation).
    Capture these rules as pseudo-detections or query templates.

5. Documentation & reporting practice
    Write short incident-style summaries for each scenario.

   Practice explaining:

    What happened.
    How it was detected.
    Potential impact.
    Recommended response and hardening actions.

   ---

✅ Skills Targeted
Working through this repository aims to strengthen:

1. Log parsing and field-based search skills.
2. Threat hunting techniques across multiple log sources.
3. Understanding of common attacker techniques:
4. Brute-force, password spray, web recon, SQLi, C2, IAM abuse, data exfiltration, log wiping.
5. Documentation and communication in a SOC context (clear, concise, evidence-based).

---

🚀 Roadmap
Planned next steps for this repo:

1. Add ready-made search query snippets for each scenario.
2. Provide detection rule ideas (pseudo-SIEM rules) based on the logs.
3. Include example investigation notes and timelines.
4. Optionally expand the dataset with:
5. More hosts and user accounts.
6. Additional attack techniques (ransomware behavior, lateral movement, persistence).

---

🤝 Contributions

This is a learning-focused project. Suggestions, improvements, and additional scenarios are welcome.
Potential contributions:
   New log scenarios (e.g., insider threat, misconfigured S3 buckets).
   Better detection query patterns.
   Sample incident reports or playbook ideas.

---

If you are interested in SOC analysis, blue teaming, or detection engineering, this repository serves as a practical mini-lab to experiment with real-world style logs and sharpen your analytical skills. 🛡️📊
