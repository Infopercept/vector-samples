# SSH Server IPv4 Listening Parser

This Vector configuration parses SSH server listening events specifically for IPv4 addresses from syslog messages.

## Overview

The configuration detects and parses log entries when the SSH server starts listening on IPv4 addresses. It extracts relevant information such as timestamp, hostname, program details, and network information.

## Input Format

The parser expects syslog messages in the following format:

```
Nov 15 11:22:33 ubuntu-server sshd[1234]: Server listening on 0.0.0.0 port 22.
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for SSH server IPv4 listening events
2. Extract timestamp, hostname, and program information
3. Parse the PID and network details
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_ipv4.json` in the following format:

```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 1234,
  "source_ip": "192.168.1.1",
  "port": 22,
  "event_type": "server_listening_ipv4",
  "ipv_version": "IPv4"
}
```

This JSON output provides a structured representation of the SSH server's IPv4 listening events, making it easier to analyze and process the log data.

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

- The parser specifically handles IPv4 listening events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
