# SSHD Invalid User Failure Parser

This Vector configuration parses SSH authentication logs to extract information about failed login attempts for invalid users.

## Overview

The configuration processes SSH authentication logs to capture failed login attempts, specifically focusing on authentication failures for invalid users. It extracts detailed information including the authentication method, user type, and protocol used.

## Input Format

The parser expects syslog messages in the following format:

```
Dec 10 13:45:23 ubuntu-server sshd[12345]: Failed password for invalid user admin from 192.168.1.100 port 54321 ssh2
```

## Configuration Details

The configuration uses Vector's remap transform to:
1. Match the syslog pattern for failed SSH authentication attempts
2. Extract timestamp, hostname, and program information
3. Parse authentication method, user type, username, source IP, port, and protocol
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entries will be written to `vector_parsed_ssh_invalid.json` in the following format:

```json
{
  "timestamp": "Dec 10 13:45:23",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 12345,
  "auth_method": "password",
  "user_type": "invalid",
  "username": "admin",
  "source_ip": "192.168.1.100",
  "port": 54321,
  "protocol": "ssh2",
  "event_type": "Invalid User Failure"
}
```

## Usage

1. Ensure Vector is properly installed on your system
2. Place the vector.yaml configuration file in your Vector configuration directory
3. Ensure the auth.log file is accessible to Vector
4. Restart Vector to apply the configuration

## Requirements

- Vector v0.44 or higher
- Access to SSH authentication logs (auth.log)
- Write permissions for the output directory

## Notes

- The parser handles both valid and invalid user authentication failures
- Failed authentication attempts are captured regardless of the authentication method
- Unparseable logs are marked with event_type "unparsed_log"
- The configuration ignores checkpoints and reads from the beginning of the log file
