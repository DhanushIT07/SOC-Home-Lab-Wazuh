# SOC Home Lab — Wazuh

A hands-on Security Operations Center (SOC) home lab built with pfSense, Wazuh, Ubuntu Server, and Kali Linux.

## Objectives

- Build a segmented SOC lab network
- Deploy Wazuh SIEM/XDR
- Onboard Linux and Windows endpoints
- Generate controlled security events
- Practice detection, investigation, and incident response
- Map findings to MITRE ATT&CK
- Document troubleshooting and lessons learned

## Lab Architecture

```
                    Internet
                       |
                    pfSense
                  192.168.10.1
                       |
                   SOC-LAB
          +------------+------------+
          |            |            |
        Kali        Ubuntu        Wazuh
      Attacker       Agent        SIEM
       .10.101       .10.102       .10.103
```

## Current Progress

- [x] VirtualBox environment
- [x] pfSense LAN / SOC-LAB network
- [x] Kali Linux endpoint
- [x] Wazuh OVA deployed
- [x] Wazuh Manager, Indexer, Dashboard verified
- [x] Ubuntu Server 24.04.5 LTS deployed
- [x] Wazuh Agent installed and running on Ubuntu
- [ ] Verify agent communication in Wazuh Dashboard
- [ ] Generate first security event
- [ ] Detection and investigation exercises
- [ ] Windows endpoint
- [ ] MITRE ATT&CK mapping
- [ ] Incident reports

## Repository Structure

- `01-infrastructure/` — network and architecture
- `02-wazuh/` — Wazuh deployment and agent onboarding
- `03-detection/` — detection exercises
- `04-investigation/` — investigation workflows
- `05-mitre-attack/` — ATT&CK mappings
- `06-incident-reports/` — incident documentation
- `screenshots/` — selected lab evidence
- `diagrams/` — architecture diagrams

> This repository intentionally excludes passwords, API keys, tokens, private keys, and other secrets.
