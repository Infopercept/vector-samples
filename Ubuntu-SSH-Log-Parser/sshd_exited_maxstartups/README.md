# SSHD Exited MaxStartups Parser

This Vector configuration parses SSH MaxStartups throttling events from Ubuntu auth.log files. It tracks when SSH server exits from MaxStartups throttling state.

## Overview

The configuration detects and parses log entries when SSH server exits from MaxStartups throttling state. It extracts relevant information such as timestamp, hostname, program details, duration of throttling, and number of dropped connections.

## Input Format

The parser expects syslog messages in the following format:

```
May 15 09:23:45 ubuntu-server sshd[12345]: exited MaxStartups throttling after 00:15:30, 50 connections dropped
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for SSH MaxStartups throttling exit events
2. Extract timestamp, hostname, and program information
3. Parse the throttling duration and number of dropped connections
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_maxstartups.json` in the following format:

```json
{
  "timestamp": "May 15 09:23:45",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 12345,
  "event_type": "maxstartups_throttling_exited",
  "duration": "00:15:30",
  "dropped_connections": 50
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

- The parser specifically handles SSH MaxStartups throttling exit events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
