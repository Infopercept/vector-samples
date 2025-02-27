# SSH Failed Login Detection using Demo Logs

This demo shows how to monitor SSH login attempts and detect potential brute force attacks using Vector.

## Overview

The setup uses Vector to:
1. Monitor authentication log files
2. Parse failed login attempts
3. Aggregate failed attempts by username and IP
4. Generate alerts for suspicious activity (3+ failed attempts)

## Configuration Details

The Vector configuration (`vector.yaml`) implements the following pipeline:

### Sources
- Monitors the local `auth.log` file for SSH authentication events

### Transforms
1. `parse_auth_log`: Extracts information from failed password attempts
2. `aggregate_failed_logins`: Groups failed attempts by username and IP
3. `detect_brute_force`: Generates alerts for 3+ failed attempts

### Sinks
- Writes alerts to `ssh_alerts.json` in JSON format

## Usage

1. Ensure Vector is installed on your system
2. Copy the `vector.yaml` configuration file to your Vector config directory
3. Start Vector:
   ```bash
   vector --config vector.yaml
   ```
4. Monitor the `ssh_alerts.json` file for suspicious login attempts

## Alert Format

Alerts are generated in JSON format with the following information:
- Username attempting to log in
- Source IP address
- Number of failed attempts
- Timestamp of detection
