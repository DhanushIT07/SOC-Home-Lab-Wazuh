# Lab Architecture

## Network

The lab uses a VirtualBox Internal Network named `SOC-LAB`.

| Component | Role | IP |
|---|---|---|
| pfSense | Firewall / gateway | 192.168.10.1 |
| Kali Linux | Attacker / analyst | 192.168.10.101 |
| SOC-Ubuntu | Monitored Linux endpoint | 192.168.10.102 |
| Wazuh | SIEM / central components | 192.168.10.103 |

## Traffic Flow

```
Kali / Ubuntu
     |
 SOC-LAB
     |
  pfSense
     |
  Internet
```

The Wazuh agent on Ubuntu is configured to communicate with the Wazuh Manager at `192.168.10.103`.

## Design Goal

Keep the SIEM separate from the monitored endpoint so the lab reflects a basic SOC architecture rather than placing all components on one host.
