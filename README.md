![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![n8n](https://img.shields.io/badge/built%20with-n8n-orange)
![Status](https://img.shields.io/badge/status-active-brightgreen)

# CTI-Enrichment-n8n: Automated SOC Workflow 

## Overview
This repository contains a Security Orchestration, Automation, and Response (SOAR) workflow built with **n8n**. It automatically enriches security alerts from SIEM/XDR platforms (like Wazuh) using **AbuseIPDB** for Cyber Threat Intelligence (CTI) and interacts with Cloud APIs (AWS) to provide business context.

## Architecture

```mermaid
graph LR
    A[Wazuh SIEM] -->|Webhook Alert| B(n8n Receiver)
    B --> C{AbuseIPDB API}
    C -->|Score > 80| D[AWS API Context]
    C -->|Score <= 80| E[Log & Discard]
    D --> F[Slack/Teams Alert]
    F -.->|Manual Approval| G[Block IP on AWS WAF]

