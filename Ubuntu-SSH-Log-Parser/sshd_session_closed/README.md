# SSHD Session Closed Parser

This Vector configuration parses SSH session closure events from syslog messages, tracking when user sessions are terminated.

## Overview

The configuration detects and parses log entries when SSH sessions are closed. It extracts relevant information such as timestamp, hostname, program details, and session information.

## Input Format

The parser expects syslog messages in the following format:

```
Nov 15 11:22:33 ubuntu-server sshd[1234]: pam_unix(sshd:session): session closed for user username
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for SSH session closed events
2. Extract timestamp, hostname, and program information
3. Parse the PAM module, activity type, and username details
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_log.json` in the following format:

```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 1234,
  "pam_module": "pam_unix",
  "pam_activity": "sshd:session",
  "event_type": "session closed",
  "username": "username"
}
```

This JSON output provides a structured representation of SSH session closure events, making it easier to analyze and process the log data.

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

- The parser specifically handles SSH session closure events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
