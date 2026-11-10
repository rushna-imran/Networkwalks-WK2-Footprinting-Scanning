# Networkwalks-WK2-Footprinting-Scanning
Hands-on passive &amp; active web footprinting, DNS enumeration, subnet scanning, ARP interrogation, and topology mapping for Networkwalks Week 2 lab curriculum.
# PENETRATION TESTING & NETWORK SCANNING REPORT

## Description & Overview
This report documents the practical security analysis executed during Week 2 (`W2-PM1` and `W2-PM5`) under the Networkwalks Cybersecurity Internship Program. All testing was executed in full compliance with explicit authorization within scoped target environments (`networkwalks.com` and isolated virtual lab subnets). The primary objective was to perform passive and active domain reconnaissance, gather target infrastructure metadata, discover active hosts on local subnets, analyze host routing, map network topology, and extract physical MAC identifiers via ARP table interrogation. Unapproved distribution or misuse of this technical data is strictly prohibited.

---

## 1. Document Metadata & Scope
- **Pentester Name:** Rushna Imran (Cybersecurity Professional)
- **Program / Batch:** Networkwalks Cybersecurity Internship
- **Date:** November 2026
- **Modules Completed:** `W2-PM1` (Multiple Kali Tools), `W2-PM5` (Zenmap Subnet Scanning)
- **Target Environments:**
  1. `networkwalks.com` (Secured written permission)
  2. Local Subnet / Virtual LAN Network (`192.168.56.0/24`)
- **Permission Status:** Explicit Authorized Access Granted
- **Phases Covered:** Phase 1 (Reconnaissance & Footprinting), Phase 2 (Scanning & Network Discovery)

---

## 2. Executive Summary & Liability Disclaimer
This report covers the execution of Week 2 tasks (`W2-PM1` and `W2-PM5`) under the Networkwalks Cybersecurity Internship Program. All activities adhered to authorized testing boundaries. The primary goal involved domain reconnaissance, infrastructure metadata gathering, subnet host discovery, and topology mapping.

---

## 3. Technical Activities & Findings

### 3.1 Domain Reconnaissance & Footprinting (Task W2-PM1)
**Target Domain:** `networkwalks.com` / `www.networkwalks.com`
- **WHOIS & DNSRecon Enumeration:** Extracted domain registrar records identifying SOA server `ns56135.hostgator.com` (`50.87.144.87`), NS records `ns56135.hostgator.com` and `ns56136.hostgator.com`, MX mail server `mail.networkwalks.com` (`192.232.216.135`), A record `192.232.216.135`, and SPF TXT policy `v=spf1 +a +mx +ip4:50.87.144.87 +include:website-welcome.com ~all`.
- **WhatWeb Fingerprinting:** `http://www.networkwalks.com` returned HTTP 301 Moved Permanently (Apache server in US), redirecting to `https://networkwalks.com/` which returned HTTP 200 OK (Apache, WordPress 7.1.4, Bootstrap 7.1.4, IP `192.232.216.135`, Title: *Networkwalks Academy*).
- **WAF Inspection (`wafw00f`):** Analyzed HTTP request/response behaviors to verify Web Application Firewall presence (ModSecurity).
- **DNS Resolution (`nslookup`):** Resolved target domain via local DNS server (`192.168.10.1#53`), confirming non-authoritative resolution for `networkwalks.com` to IP `192.232.216.135`.
- **HTTP Header Analysis (`curl -I`):** Extracted HTTP/2 200 OK headers revealing `server: Apache`, `x-powered-by: PHP/7.4.33`, `x-endurance-cache-level: 0`, and permissions-policy parameters.

### 3.2 Subnet Discovery & Topology Mapping (Task W2-PM5)
**Target Network:** Local Virtual Subnet (`192.168.56.0/24`)
- Executed Nmap host discovery (`-sn`) and intense scan profiles via Zenmap GUI across the target subnet.
- Identified active live host (`192.168.56.1`) and verified open port profiles and running service banners.
- Extracted physical interface hardware addresses using local ARP table interrogation (`arp -a`).
- Rendered visual network topology diagrams using Zenmap's interactive graph visualizer and exported graphic vector files (`zenmappgraphics.pdf`).

---

## 4. Risk Analysis & Threat Impact
- **Passive Reconnaissance Information Exposure:** Publicly accessible DNS, MX, and WHOIS metadata allow external attackers to map corporate web infrastructure without triggering intrusion alarms.
- **Internal Subnet Exposure:** Open ports and unsegmented broadcast domains allow potential lateral movement once an initial network foothold is gained.

---

## 5. Security Recommendations
1. Implement WHOIS privacy protection on corporate domains to obscure administrative contact vectors.
2. Enforce internal network micro-segmentation (VLANs) and ARP inspection controls to limit lateral discovery.
3. Harden exposed web servers and update Web Application Firewall (WAF) filtering rulesets.

---

## 6. Conclusion
All Phase 1 and Phase 2 tasks specified in the Week 2 curriculum were successfully executed and validated. Technical evidence including CLI output logs, host IP/MAC tables, screenshot captures, and exported topology graphics have been compiled for portfolio verification.

---

## 7. Tools & Command Reference
The following table outlines all command-line tools and utilities deployed during this security assessment, detailing their specific technical purpose:

| Command / Tool | Technical Purpose & Operational Context |
| :--- | :--- |
| **`whois networkwalks.com`** | Queries public domain registrars to retrieve ownership details, administrative contacts, creation dates, and authoritative name servers. |
| **`dnsrecon -d networkwalks.com`** | Enumerates DNS infrastructure records (A, MX, NS, SOA, TXT/SPF) to map public routing and mail handling servers. |
| **`nslookup networkwalks.com`** | Performs direct DNS queries to map hostnames to IP addresses and verify local DNS server responses. |
| **`whatweb www.networkwalks.com`** | Fingerprints target web applications, identifying web server software (Apache), CMS versions (WordPress), and backend frameworks. |
| **`wafw00f https://networkwalks.com`** | Probes target endpoints with crafted HTTP requests to detect Web Application Firewalls (WAF) protecting the web application. |
| **`curl -I https://networkwalks.com`** | Fetches HTTP response headers only to inspect web server banners, PHP runtime versions, and caching rules. |
| **`ping -c 4 8.8.8.8`** | Sends ICMP echo requests to verify basic network-layer connectivity and DNS reachability before executing scans. |
| **`nmap -sn 192.168.56.0/24` / Zenmap** | Scans subnets to perform host discovery, port scanning, service versioning, and visual network topology generation. |
| **`arp -a`** | Queries the local ARP cache to map IP addresses to physical MAC hardware addresses across the network segment. |

---

## 8. Evidences Collected (in the google docs PDF down below!)
- Terminal log outputs (`dnsrecon`, `nslookup`, `whatweb`, `curl -I`, `whois`, `Nmap/Zenmap`).
- Local ARP table mapping outputs.
- Topology graphic PDF export (`zenmappgraphics.pdf`).
- Technical troubleshooting logs (Hypervisor screen captures, DNS resolution handling).

---

### **Author & Reference Information**
- **Author:** Rushna Imran (Intern ID: `NW-084-318`)
- **LinkedIn Profile:** [https://www.linkedin.com/in/rushna-imran-3338303b6/)
- **Google Docs Report:** [W2-PM-FINAL - Network Footprinting & Scanning Report](https://doc-0g-74-docstext.googleusercontent.com/export/detnt47uao87g8t8pdbtqa5ako/r93n5mhpjicumhrualtguj2ufo/1794271070000/102014739901915846429/102014739901915846429/1UILIKWT0leMKZnzDwv-WsNZgSdwEoZPRoIjbTi5rRWk?format=pdf&id=1UILIKWT0leMKZnzDwv-WsNZgSdwEoZPRoIjbTi5rRWk&token=AMtJHwlPyzqOO5j-Tprw3iKo6uxN:1794269557428&ouid=102014739901915846429&includes_info_params=true&cros_files=false&nded=false&tab=t.0&ettp=1&dat=ALtZeknaWqlnVWOIvKFF-ZISdLTz5RxbHaqcI97FvyJK3xs0a5w8Kl28tdqRhJVbcZBlm8IGCXJDhwgtqFJmvTc8QJ6HAzWLutYUEO-8nYrfOdEAvr2QuMebF9bY3h-b4rzxMDFYKqADhHS8LBmlF4xukSmLg1o4CBbA5c1AgFgoYemYNI3DlmpiPa_4KHDvy8D_arp8wrILXz3fRDXC1hXTiGTr4qTtp4DcIFMFqneX-GQ2l8gI9Ly2jBGzGmNisalBdmGArUOrLdlfaTz7M9Xfxgk7ZNtu2nKbC_2VB7mrF_GFfkSWXdmCUuaW4Ex35-fRTbA281S9tp_wX-0K2bF9xktVHnMprczkoE0CdFvnkX-f7xRWNcQIKcGn3Vazzf16sPn1BAxe9ShVyinncwBo9ed4FqIZBrca2WquFXyg0p-lkmjrUl3ZM1qhY_D6iX-9HHp9wGG5nAhqS27-VtF8AQjb8P2u1M_7uR-tXCSsn5QAvGbukizAa1GjWCq1BsD5ShcHSmBGuNqGFdF1T1JULR_5zTO7jyJOtNCZ4AIAxgjwlv_dl2FmKEAEd39Pw7uwMFoF0HOoz0yluuAmQUKbuts33pO3AeRuwMR6RWOjbv_RTI5dEgFIJaQmq0eoYd_CGnnih3hT6GNEPcC0fSLIvA5Jk2eFV2Xs2G56WrfPnLGtRjbNQFC_2iWbE93K5JmTMWjkpJApryd_XGd6L_BnPgWNEDyBklNjqkTeTLGGLKAlswF9ah9WCx8AbUHSx1tzT40j_pEvC5jk13gvH-QsNJwTwaLQtviVAN-7xys1SvdMGFSNsdLZEcM2dSbP36jyo2qXU7LiFUtsFiCRG-fHG5jfYr8sxV_aOmyWfsLLjp4YCWZ4Scg1XFAs7yOG0s1wLLDV_zCdNU6-3F7CNhU_68gJ6Iot7u1-d7ImOlj9XmlNWliaIoS3A7W9-xA_banofjBkBtsgp-fXCPfAWm0fXLQVCGr9Lz2UB8BclW_YdJZ7bg2H8wuNTAiBerZ5WA)
