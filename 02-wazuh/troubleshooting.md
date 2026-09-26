# Wazuh Troubleshooting Notes — Day 1

## Issue: Unable to locate package

Command:

```bash
sudo WAZUH_MANAGER="192.168.10.103" apt install wazuh-agent
```

Error:

```
Unable to locate package wazuh-agent
```

### Investigation

Checked repository configuration, keyring location, APT source filename, DNS, and network connectivity.

### Root Cause

APT was ignoring the Wazuh repository because the source file was created incorrectly.

### Fix

Use:

```
/etc/apt/sources.list.d/wazuh.list
```

Then run:

```bash
sudo apt update
apt-cache policy wazuh-agent
```

After the package became available, installation succeeded.

## Key Lesson

An error message should be treated as evidence. Verify each dependency rather than repeatedly running the same installation command.
