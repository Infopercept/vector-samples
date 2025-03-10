# SSHD Drop Connection Parser

This Vector configuration parses SSH connection drop events from Ubuntu auth.log files. It tracks when SSH connections are dropped by the server.

## Overview

The configuration detects and parses log entries when SSH connections are dropped. It extracts relevant information such as timestamp, hostname, program details, and connection information including source and destination details.

## Input Format

The parser expects syslog messages in the following format:

```
May 15 09:23:45 ubuntu-server sshd[12345]: drop connection #789 from [192.168.1.100]:54321 on [10.0.0.1]:22 invalid user
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for SSH connection drop events
2. Extract timestamp, hostname, and program information
3. Parse the connection ID, source IP/port, and destination IP/port
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_ssh_connection_drop.json` in the following format:

```json
{
  "timestamp": "May 15 09:23:45",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 12345,
  "event_type": "dropped connection",
  "connection_id": 789,
  "source_ip": "192.168.1.100",
  "source_port": 54321,
  "destination_ip": "10.0.0.1",
  "destination_port": 22,
  "reason": "invalid user"
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

- The parser specifically handles SSH connection drop events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
