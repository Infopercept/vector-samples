# SSHD Authentication Failure Log Parser

This Vector configuration parses Ubuntu's auth.log entries specifically for SSH authentication failures using PAM (Pluggable Authentication Modules).

## Overview

The configuration captures and processes SSH authentication failure events from auth.log, extracting detailed information about failed login attempts including user details and remote connection information.

## Input Format

The parser expects syslog messages in the following format:

```
Aug 15 14:23:45 ubuntu-server sshd[12345]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.1.100
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Monitor the auth.log file for new entries
2. Parse authentication failure messages using regex
3. Extract comprehensive authentication details
4. Structure the data into a standardized JSON format

### Extracted Fields
- Timestamp
- Hostname
- Program name and PID
- PAM module and details
- User information (logname, uid, euid)
- Connection details (tty, ruser, rhost)

### Sample Output

The parsed log entry will be written to `vector_parsed_auth_failure.json` in the following format:

```json
{
  "timestamp": "Aug 15 14:23:45",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 12345,
  "pam_module": "pam_unix",
  "pam_details": "sshd:auth",
  "reason": "authentication failure",
  "logname": "",
  "uid": 0,
  "euid": 0,
  "tty": "ssh",
  "ruser": "",
  "rhost": "192.168.1.100",
  "event_type": "pam_unix_authentication_failure"
}
```

## Usage

1. Ensure Vector is properly installed on your system
2. Place the vector.yaml configuration in your Vector configuration directory
3. Verify read access to auth.log
4. Update file paths if necessary
5. Start Vector with this configuration

## Requirements

- Vector v0.44 or higher
- Read access to auth.log
- Write permissions for output directory

## Notes

- The parser focuses specifically on SSH authentication failures
- Ensure log format matches the expected pattern
- Monitor the output file for parsed events
- Adjust file paths in the configuration as needed for your system