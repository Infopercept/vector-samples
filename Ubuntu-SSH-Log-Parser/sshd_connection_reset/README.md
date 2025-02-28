# SSHD Connection Reset Log Parser

This Vector configuration parses Ubuntu's auth.log entries specifically for SSH connection reset events.

## Overview

The configuration detects and parses log entries when SSH connections are reset. It can handle both regular users and specifically identifies invalid or authenticating users.

## Input Format

The parser expects syslog messages in the following formats:

```
Aug 15 14:23:45 ubuntu-server sshd[12345]: Connection reset by invalid user admin 192.168.1.100 port 54321 [preauth]
Aug 15 14:23:45 ubuntu-server sshd[12345]: Connection reset by authenticating user admin 192.168.1.100 port 54321 [preauth]
Aug 15 14:23:45 ubuntu-server sshd[12345]: Connection reset by admin 192.168.1.100 port 54321 [preauth]
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for connection reset events
2. Extract timestamp, hostname, and program information
3. Parse user type (invalid/authenticating if present), username, source IP, port, and status
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_log.json` in the following format:

```json
{
  "timestamp": "Aug 15 14:23:45",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 12345,
  "event_type": "Connection reset",
  "user_type": "invalid",
  "username": "admin",
  "source_ip": "192.168.1.100",
  "port": 54321,
  "status": "preauth"
}
```

The `user_type` field will only be present if the user is specifically marked as "invalid" or "authenticating" in the log.

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

- The parser handles all types of SSH connection reset events
- The regex pattern is flexible to accommodate optional user type information
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
