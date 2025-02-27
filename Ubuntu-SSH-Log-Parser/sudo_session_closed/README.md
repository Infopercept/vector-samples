# Sudo Session Closed Parser

This Vector configuration parses sudo session closure events from authentication logs, tracking when privileged sessions end.

## Overview

The configuration detects and parses log entries when sudo sessions are closed for users. It extracts relevant information such as timestamp, hostname, program details, and session information.

## Input Format

The parser expects syslog messages in the following format:

```
Nov 15 11:22:33 ubuntu-server sudo: pam_unix(sudo:session): session closed for user rootuser
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for sudo session closure events
2. Extract timestamp, hostname, and program information
3. Parse the PAM module, activity type, and session user details
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_log.json` in the following format:

```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "sudo",
  "appname": "sudo",
  "pam_module": "pam_unix",
  "pam_activity": "sudo:session",
  "session_user": "rootuser",
  "event_type": "session_closed",
  "host": "localhost.localdomain",
  "source_type": "file"
}
```

This JSON output provides a structured representation of sudo session closure events, making it easier to analyze and process the log data.

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

- The parser specifically handles sudo session closure events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
