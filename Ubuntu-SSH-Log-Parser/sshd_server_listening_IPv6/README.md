# SSHD Server IPv6 Listening Parser

This Vector configuration parses SSH server listening events specifically for IPv6 addresses from syslog messages.

## Overview

The configuration detects and parses log entries when the SSH server starts listening on IPv6 addresses. It extracts relevant information such as timestamp, hostname, program details, and network information.

## Input Format

The parser expects syslog messages in the following format:

```
Nov 15 11:22:33 ubuntu-server sshd[1234]: Server listening on :: port 22.
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for SSH server IPv6 listening events
2. Extract timestamp, hostname, and program information
3. Parse the PID and network details
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_ipv6.json` in the following format:

```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 1234,
  "source_ip": "::",
  "port": 22,
  "event_type": "server_listening_ipv6",
  "ipv_version": "IPv6"
}
```

This JSON output provides a structured representation of the SSH server's IPv6 listening events, making it easier to analyze and process the log data.

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

- The parser specifically handles IPv6 listening events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
