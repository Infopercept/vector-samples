# SSHD Invalid User Parser

This Vector configuration parses SSH authentication logs to extract information about invalid user login attempts.

## Overview

The configuration detects and parses log entries when SSH login attempts are made with invalid usernames. It extracts relevant information such as timestamp, hostname, program details, and authentication attempt information.

## Input Format

The parser expects syslog messages in the following format:

```
Dec 10 13:45:23 ubuntu-server sshd[12345]: Invalid user admin from 192.168.1.100 port 54321
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for invalid SSH user attempts
2. Extract timestamp, hostname, and program information
3. Parse the invalid username, source IP, and port details
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_invalid_user.json` in the following format:

```json
{
  "timestamp": "Dec 10 13:45:23",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 12345,
  "username": "admin",
  "source_ip": "192.168.1.100",
  "port": 54321,
  "event_type": "invalid_user"
}
```

This JSON output provides a structured representation of invalid SSH user attempts, making it easier to analyze and process the log data.

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

- The parser specifically handles invalid SSH user attempts
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
