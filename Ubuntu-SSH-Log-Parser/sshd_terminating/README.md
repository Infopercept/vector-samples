# SSHD Terminating Signal Parser

This Vector configuration parses SSH termination events when the SSH daemon receives signals to terminate or restart.

## Overview

The configuration detects and parses log entries when the SSH daemon receives system signals. It extracts relevant information such as timestamp, hostname, program details, and signal information.

## Input Format

The parser expects syslog messages in the following format:

```
Nov 15 11:22:33 ubuntu-server sshd[1234]: Received signal 15; terminating.
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for SSH signal reception events
2. Extract timestamp, hostname, and program information
3. Parse the signal number and termination message
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_log.json` in the following format:

```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 1234,
  "signal": 15,
  "reason": "terminating",
  "event_type": "ssh_signal"
}
```

This JSON output provides a structured representation of SSH termination events, making it easier to analyze and process the log data.

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

- The parser specifically handles SSH daemon signal events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
