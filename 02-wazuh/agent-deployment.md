# Wazuh Agent Deployment — Ubuntu

## Objective

Install the Wazuh Agent on the Ubuntu 24.04.5 LTS monitored endpoint and configure it to use the Wazuh Manager at `192.168.10.103`.

## Repository Setup

Create the Wazuh keyring:

```bash
curl -fsSL https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo gpg --dearmor -o /usr/share/keyrings/wazuh.gpg
```

Set permissions:

```bash
sudo chmod 644 /usr/share/keyrings/wazuh.gpg
```

Add the Wazuh APT repository:

```bash
echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
```

Update package metadata:

```bash
sudo apt update
```

Verify the package is available:

```bash
apt-cache policy wazuh-agent
```

## Installation

```bash
sudo WAZUH_MANAGER="192.168.10.103" apt install wazuh-agent
```

Enable and start the service:

```bash
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

Verify:

```bash
sudo systemctl status wazuh-agent --no-pager
```

## Current Result

Wazuh Agent 4.14.8-1 was installed successfully and the service reported:

```
Active: active (running)
```

The next step is to verify that the agent is communicating with the Wazuh Manager and appears in the Wazuh Dashboard.

## Troubleshooting

### Package not found

Initial installation returned:

```
E: Unable to locate package wazuh-agent
```

Cause: the Wazuh APT repository was not being read correctly.

### Wrong source-list directory

An incorrect path was used:

```
/etc/apt/source.list.d/
```

Correct path:

```
/etc/apt/sources.list.d/
```

### Repository file without extension

An initial repository file was named:

```
/etc/apt/sources.list.d/wazuh
```

APT ignored it because it had no filename extension.

Correct filename:

```
/etc/apt/sources.list.d/wazuh.list
```

### GPG option error

An early command used the invalid option `--keyrings`. The correct GPG option is `--keyring`.

The key was ultimately created correctly with `gpg --dearmor` into `/usr/share/keyrings/wazuh.gpg`.

### DNS troubleshooting

At one point `packages.wazuh.com` could not be resolved. Connectivity was tested separately using the gateway, public IP connectivity, and DNS hostname resolution before continuing.

## Lessons Learned

Troubleshoot in layers:

1. Local interface
2. Gateway
3. Internet connectivity
4. DNS
5. Repository configuration
6. Package availability
7. Service state
8. Application-level communication
