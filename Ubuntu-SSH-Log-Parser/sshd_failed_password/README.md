# SSHD Failed Password Parser

This Vector configuration parses SSH failed password attempts from Ubuntu auth.log files. It tracks failed login attempts and invalid user authentication events.

## Overview

The configuration detects and parses log entries for failed SSH password attempts. It extracts relevant information such as timestamp, hostname, program details, and authentication attempt information.

## Input Format

The parser expects syslog messages in the following format:

```
May 15 09:23:45 ubuntu-server sshd[12345]: Failed password for invalid user test from 192.168.1.100 port 54321 ssh2
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for SSH failed password events
2. Extract timestamp, hostname, and program information
3. Parse the username, source IP, port, and protocol details
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_log.json` in the following format:

```json
{
  "timestamp": "May 15 09:23:45",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 12345,
  "event_type": "Failed password for invalid user",
  "username": "test",
  "source_ip": "192.168.1.100",
  "port": 54321,
  "protocol": "ssh2"
}
```

This JSON output provides a structured representation of failed SSH password attempts, making it easier to analyze and monitor potential security threats.

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

- The parser handles both invalid user attempts and failed passwords for valid users
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
