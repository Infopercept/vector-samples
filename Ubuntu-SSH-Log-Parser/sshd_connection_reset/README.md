# SSHD Connection Reset Log Parser

This Vector configuration parses Ubuntu's auth.log entries specifically for SSH connection reset events.

## Overview

The configuration detects and parses log entries when SSH connections are reset, particularly focusing on invalid user attempts. It extracts relevant information such as timestamp, hostname, program details, and connection information.

## Input Format

The parser expects syslog messages in the following format:

```
Aug 15 14:23:45 ubuntu-server sshd[12345]: Connection reset by invalid user admin 192.168.1.100 port 54321 [preauth]
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for connection reset events
2. Extract timestamp, hostname, and program information
3. Parse username, source IP, port, and connection status
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_log.json` in the following format:

```json
{
  "timestamp": "Aug 15 14:23:45",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 12345,
  "event_type": "Connection reset by invalid user",
  "username": "admin",
  "source_ip": "192.168.1.100",
  "port": 54321,
  "status": "preauth"
}
```

This JSON output provides a structured representation of SSH connection reset events, making it easier to analyze and monitor failed connection attempts.

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

- The parser specifically handles SSH connection reset events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
