# SSHD Authentication Failure Log Parser

This Vector configuration parses Ubuntu's auth.log entries specifically for SSH authentication failure events.

## Overview

The configuration detects and processes PAM authentication failure messages from SSH login attempts, extracting detailed information about the failed authentication events.

## Input Format

The parser expects syslog messages in the following format:

```
Feb 20 10:48:24 mihir-ubuntu sshd[15112]: pam_unix(sshd:auth): authentication failure; logname=js uid=0 euid=0 tty=ssh ruser= rhost=192.168.186.1
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for PAM authentication failures
2. Extract timestamp, hostname, and program information
3. Parse PAM-specific details including module name, authentication status
4. Capture user context information (logname, uid, euid, tty, remote host)
5. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_auth_failure.json` in the following format:

```json
{
  "timestamp": "Feb 20 10:48:24",
  "hostname": "mihir-ubuntu",
  "program": "sshd",
  "appname": "sshd",
  "pid": 15112,
  "pam_module": "pam_unix",
  "pam_details": "sshd:auth",
  "reason": "authentication failure",
  "logname": "js",
  "uid": 0,
  "euid": 0,
  "tty": "ssh",
  "ruser": "",
  "rhost": "192.168.186.1",
  "user": "admin",
  "event_type": "pam_unix_authentication_failure"
}
```

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

- The parser specifically handles PAM authentication failure messages
- All fields are extracted into a structured format for easy analysis
- The configuration includes error logging for unparseable messages
- Handles both cases where user field is present or absent
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
