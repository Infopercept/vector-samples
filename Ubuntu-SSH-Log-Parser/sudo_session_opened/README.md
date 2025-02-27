# Sudo Session Opened Parser

This Vector configuration parses sudo session opened events from authentication logs, tracking when privileged sessions begin.

## Overview

The configuration detects and parses log entries when sudo sessions are opened for users. It extracts relevant information such as timestamp, hostname, program details, and user session information.

## Input Format

The parser expects syslog messages in the following format:

```
Nov 15 11:22:33 ubuntu-server sudo: pam_unix(sudo:session): session opened for user rootuser(uid=0) by admin(uid=1000)
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for sudo session opened events
2. Extract timestamp, hostname, and program information
3. Parse the PAM module, user details, and UID information
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_session.json` in the following format:

```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "sudo",
  "appname": "sudo",
  "pam_module": "pam_unix",
  "pam_activity": "sudo:session",
  "target_user": "rootuser",
  "username": "admin",
  "target_uid": 0,
  "actor_uid": 1000,
  "event_type": "session_opened"
}
```

This JSON output provides a structured representation of sudo session opened events, making it easier to analyze and process the log data.

## Usage

1. Ensure Vector is properly installed on your system
2. Copy the configuration to your Vector configuration directory
3. Update the input and output paths as needed
4. Restart Vector to apply the changes

## Requirements

- Vector v0.44 or higher
- System with authentication logs
- Write permissions for output directory

## Notes

- The parser specifically handles sudo session opened events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
