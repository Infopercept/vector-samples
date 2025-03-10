# SSHD Beginning MaxStartups Parser

This Vector configuration parses SSH authentication logs to extract information about MaxStartups throttling events.

## Overview

The configuration detects and parses log entries related to SSH MaxStartups throttling, which occurs when the maximum number of unauthenticated connections is reached. It extracts relevant information such as timestamp, hostname, and program details.

## Input Format

The parser expects syslog messages in the following format:

```
Dec 10 13:45:23 ubuntu-server sshd[12345]: INFO: Beginning MaxStartups throttling
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for MaxStartups throttling events
2. Extract timestamp, hostname, and program information
3. Identify the log level and message content
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_ssh_maxstartups.json` in the following format:

```json
{
  "timestamp": "Dec 10 13:45:23",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 12345,
  "log_level": "INFO",
  "event_type": "beginning maxStartups throttling"
}
```

This JSON output provides a structured representation of SSH MaxStartups throttling events, making it easier to monitor and analyze SSH connection limits.

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

- The parser specifically handles MaxStartups throttling events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
