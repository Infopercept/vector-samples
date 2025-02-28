# SSHD PAM Authentication Failure Log Parser

This Vector configuration parses Ubuntu's auth.log entries specifically for PAM authentication failure events.

## Overview

The configuration detects and parses log entries when PAM authentication failures occur. It captures detailed information about the authentication attempt, including user details, process information, and host data.

## Input Format

The parser expects syslog messages in the following format:

```
Aug 15 14:23:45 ubuntu-server sshd[12345]: PAM 2 more authentication failures; logname=root uid=0 euid=0 tty=ssh ruser=root rhost=192.168.1.100 user=admin
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for PAM authentication failure events
2. Extract timestamp, hostname, and program information
3. Parse authentication details including logname, UIDs, TTY information, and remote user/host data
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
  "event": "PAM 2 more authentication failures",
  "logname": "root",
  "uid": 0,
  "euid": 0,
  "tty": "ssh",
  "ruser": "root",
  "rhost": "192.168.1.100",
  "user": "admin"
}
```

Note that the `user` field is optional and will only be present if specified in the log entry.

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

- The parser handles both singular and plural forms of "failure(s)"
- The regex pattern accommodates optional user information
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
