# Usermod Shell Change Parser

This Vector configuration parses user shell modification events from system logs when the usermod command changes a user's login shell.

## Overview

The configuration detects and parses log entries when user shell changes occur through usermod. It extracts relevant information such as timestamp, hostname, program details, and shell modification details.

## Input Format

The parser expects syslog messages in the following format:

```
Nov 15 11:22:33 ubuntu-server usermod[1234]: change user 'username' shell from '/bin/bash' to '/bin/zsh'
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for usermod shell change events
2. Extract timestamp, hostname, and program information
3. Parse the username and shell modification details
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_usermod.json` in the following format:

```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "usermod",
  "appname": "usermod",
  "pid": 1234,
  "user": "username",
  "old_shell": "/bin/bash",
  "new_shell": "/bin/zsh",
  "event_type": "usermod_change_user_shell"
}
```

This JSON output provides a structured representation of user shell modification events, making it easier to analyze and process the log data.

## Usage

1. Ensure Vector is properly installed on your system
2. Copy the configuration to your Vector configuration directory
3. Update the input and output paths as needed
4. Restart Vector to apply the changes

## Requirements

- Vector v0.44 or higher
- System with authentication logs
- Write permissions for output directory

## Notes

- The parser specifically handles usermod shell change events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
