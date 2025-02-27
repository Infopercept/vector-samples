# SSHD Received Disconnect Parser

This Vector configuration parses SSH disconnect messages from syslog entries when remote clients terminate their connections.

## Overview

The configuration detects and parses log entries when SSH clients disconnect from the server. It extracts relevant information such as timestamp, hostname, program details, and disconnect information.

## Input Format

The parser expects syslog messages in the following format:

```
Mar 15 06:25:33 hostname sshd[1234]: Received disconnect from 192.168.1.1 port 54321:11: disconnected by user
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for SSH received disconnect events
2. Extract timestamp, hostname, and program information
3. Parse the disconnect IP, port, and reason details
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_received_disconnect.json` in the following format:

```json
{
  "timestamp": "2024-03-15T06:25:33Z",
  "hostname": "hostname",
  "program": "sshd",
  "appname": "sshd",
  "pid": 1234,
  "disconnect_ip": "192.168.1.1",
  "port": 54321,
  "disconnect_code": 11,
  "reason": "disconnected by user",
  "event_type": "disconnect"
}
```

This JSON output provides a structured representation of SSH received disconnect events, making it easier to analyze and process the log data.

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

- The parser specifically handles received disconnect events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system