# Systemd New Session Parser

This Vector configuration parses systemd-logind new session events from syslog messages, tracking user session creation.

## Overview

The configuration detects and parses log entries when systemd-logind creates new user sessions. It extracts relevant information such as timestamp, hostname, program details, and session information.

## Input Format

The parser expects syslog messages in the following format:

```
Nov 15 11:22:33 ubuntu-server systemd-logind[1234]: New session 5678 of user username.
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for systemd new session events
2. Extract timestamp, hostname, and program information
3. Parse the session ID and username details
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_systemd_logind.json` in the following format:

```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "systemd-logind",
  "appname": "systemd-logind",
  "pid": 1234,
  "session_id": 5678,
  "username": "username",
  "event_type": "new session"
}
```

This JSON output provides a structured representation of systemd new session events, making it easier to analyze and process the log data.

## Usage

1. Ensure Vector is properly installed on your system
2. Copy the configuration to your Vector configuration directory
3. Update the input and output paths as needed
4. Restart Vector to apply the changes

## Requirements

- Vector v0.44 or higher
- System with systemd-logind logs
- Write permissions for output directory

## Notes

- The parser specifically handles systemd new session events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
