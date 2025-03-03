# SSHD Failed Password Repeated Log Parser

This Vector configuration parses Ubuntu's auth.log entries specifically for repeated SSH failed password attempts.

## Overview

The configuration detects and processes repeated failed password messages from SSH login attempts, extracting detailed information about multiple failed login events that were consolidated into a single log entry.

## Input Format

The parser expects syslog messages in the following format:

```
Aug 15 14:23:45 ubuntu-server sshd[12345]: message repeated 3 times: [ Failed password for admin from 192.168.1.100 port 54321 ssh2]
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for repeated failed password messages
2. Extract timestamp, hostname, and program information
3. Parse the repeat count and inner message details
4. Capture authentication details (username, source IP, port, protocol)
5. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_repeated_message.json` in the following format:

```json
{
  "timestamp": "Aug 15 14:23:45",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "app_name": "sshd",
  "pid": 12345,
  "repeat_times": 3,
  "reason": "Failed password",
  "username": "admin",
  "source_ip": "192.168.1.100",
  "port": 54321,
  "protocol": "ssh2",
  "event_type": "Failed password repeated"
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

- The parser specifically handles repeated failed password messages
- All fields are extracted into a structured format for easy analysis
- The configuration includes error logging for unparseable messages
- This configuration is particularly useful for detecting potential brute force attacks
- Adjust file paths in the configuration according to your system
