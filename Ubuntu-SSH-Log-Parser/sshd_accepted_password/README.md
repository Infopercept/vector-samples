# SSHD Accepted Password Parser

This Vector configuration parses SSH successful login events with password authentication from syslog messages.

## Overview

The configuration detects and parses log entries when users successfully authenticate via SSH using password authentication. It extracts relevant information such as timestamp, hostname, program details, and connection information.

## Input Format

The parser expects syslog messages in the following format:

```
Nov 15 11:22:33 ubuntu-server sshd[1234]: Accepted password for username from 192.168.1.100 port 54321 ssh2
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for SSH password authentication events
2. Extract timestamp, hostname, and program information
3. Parse the username, source IP, and port details
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_accepted.json` in the following format:

```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 1234,
  "username": "username",
  "source_ip": "192.168.1.100",
  "source_port": 54321,
  "auth_method": "password",
  "event_type": "accepted_password",
  "protocol": "ssh2"
}
```

This JSON output provides a structured representation of successful SSH password authentication events, making it easier to analyze and process the log data.

## Usage

1. Ensure Vector is properly installed on your system
2. Copy the configuration to your Vector configuration directory
3. Update the input and output paths as needed
4. Restart Vector to apply the changes

## Requirements

- Vector v0.44 or higher
- System with SSH server logs
- Write permissions for output directory

## Notes

- The parser specifically handles successful password authentication events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
