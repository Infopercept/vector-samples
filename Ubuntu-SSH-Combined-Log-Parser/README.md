# Ubuntu SSH Combined Log Parser

This Vector configuration provides comprehensive parsing of SSH-related log entries from Ubuntu system logs. It handles various SSH events including login attempts, connections, disconnections, and authentication events.

## Overview

The configuration processes authentication logs to extract detailed information about SSH activities, user sessions, and system authentication events. It parses multiple event types and structures them into a standardized JSON format.

## Supported Event Types

The parser handles the following types of events:
- Login attempts
- Connection resets
- User disconnections
- Failed password attempts
- Invalid user attempts
- Successful password authentications
- Session management (open/close)
- User/Group modifications
- PAM authentication events
- SSH server events
- Signal handling events

## Input Format

The parser expects syslog format messages. Examples of supported log entries:

```
Nov 15 11:22:33 hostname sshd[1234]: Attempted login by user1 (UID: 1000) on pts/0
Nov 15 11:22:33 hostname sshd[1234]: Failed password for invalid user test from 192.168.1.100 port 54321 ssh2
Nov 15 11:22:33 hostname sshd[1234]: Accepted password for user1 from 192.168.1.100 port 54321 ssh2
```

## Configuration Details

The configuration uses Vector's remap transforms to:
1. Match various log patterns using regex
2. Extract relevant fields like timestamp, hostname, and program details
3. Parse event-specific information
4. Structure data into consistent JSON format
5. Categorize events by type

### Sample Output

The parsed log entries will be written to `vector_parsed_logs.json` in the following format:

```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 1234,
  "event_type": "Failed password",
  "username": "test",
  "source_ip": "192.168.1.100",
  "port": 54321,
  "protocol": "ssh2"
}
```

## Usage

1. Ensure Vector is installed on your system
2. Copy the configuration to your Vector configuration directory
3. Update the input path to point to your auth.log file
4. Update the output path as needed
5. Restart Vector to apply the changes

## Requirements

- Vector v0.44 or higher
- Access to Ubuntu authentication logs
- Write permissions for the output directory

## Notes

- The parser handles a wide range of SSH and authentication-related events
- Each event type has specific fields relevant to that event
- Unknown log formats are marked with event_type "unknown"
- Make sure log formats match your system's configuration
