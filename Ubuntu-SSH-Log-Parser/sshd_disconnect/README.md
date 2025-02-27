# SSHD Disconnect Parser

This Vector configuration parses SSH disconnect events from Ubuntu auth.log files. It tracks when users disconnect from SSH sessions.

## Overview

The configuration detects and parses log entries when users disconnect from SSH sessions. It extracts relevant information such as timestamp, hostname, program details, and connection information.

## Input Format

The parser expects syslog messages in the following format:

```
May 15 09:23:45 ubuntu-server sshd[12345]: Disconnected from user john 192.168.1.100 port 54321
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for SSH disconnect events
2. Extract timestamp, hostname, and program information
3. Parse the username, source IP, and port details
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_disconnect.json` in the following format:

```json
{
  "timestamp": "May 15 09:23:45",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 12345,
  "event_type": "Disconnected",
  "username": "john",
  "disconnect_ip": "192.168.1.100",
  "port": 54321
}
```

This JSON output provides a structured representation of SSH disconnect events, making it easier to analyze and process the log data.

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

- The parser specifically handles SSH disconnect events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
