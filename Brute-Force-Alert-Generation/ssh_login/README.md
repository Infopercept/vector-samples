# SSH Login Monitoring System

This project implements real-time SSH login attempt monitoring using Vector to detect potential brute force attacks.

## Features

- Real-time monitoring of `/var/log/secure` for SSH authentication events
- Detection of failed login attempts
- Aggregation of failed attempts by username and IP address
- Alerts for suspicious activity (3+ failed attempts)
- Dual output to both file and console for easy monitoring

## Configuration Overview

The system uses Vector (`vector.yaml`) with the following components:

### Sources
- Monitors system authentication logs from `/var/log/secure`
- Configured to read from the beginning of the log file

### Transforms
1. **parse_auth_log**: 
   - Extracts relevant information from failed password attempts
   - Captures username, IP address, port, and protocol

2. **aggregate_failed_logins**:
   - Groups failed attempts by username and IP
   - Uses a 60-second window for aggregation
   - Maintains up to 1000 events in memory

3. **detect_brute_force**:
   - Triggers alerts for 3 or more failed attempts
   - Generates detailed alert messages

### Sinks
1. **file_sink**: 
   - Writes alerts to `ssh_alerts.json`
   - Uses JSON encoding for structured data

2. **console_sink**:
   - Outputs alerts to console in real-time
   - Useful for immediate monitoring

## Setup

1. Ensure Vector is installed and configured
2. Place the `vector.yaml` in Vector's configuration directory
3. Ensure Vector has permission to read `/var/log/secure`
4. Start Vector:
   ```bash
   vector --config vector.yaml
   ```

## Monitoring

- Check `ssh_alerts.json` for persistent alert history
- Watch console output for real-time alerts
- Alerts include username, source IP, and attempt count