# Sudo Command Execution Parser

This Vector configuration parses sudo command execution events from authentication logs, tracking privileged command usage.

## Overview

The configuration detects and parses log entries when users execute commands using sudo. It extracts relevant information such as timestamp, hostname, user details, and command execution information.

## Input Format

The parser expects syslog messages in the following format:

```
Nov 15 11:22:33 ubuntu-server sudo: username : TTY=pts/0 ; PWD=/home/user ; USER=root ; COMMAND=/usr/sbin/usermod -s /bin/bash targetuser
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for sudo command execution events
2. Extract timestamp, hostname, and user information
3. Parse the TTY, working directory, target user, and command details
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_sudo.json` in the following format:

```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "sudo",
  "appname": "sudo",
  "username": "username",
  "tty": "pts/0",
  "pwd": "/home/user",
  "target_user": "root",
  "command": "/usr/sbin/usermod -s /bin/bash targetuser",
  "event_type": "sudo_command_executed"
}
```

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

- The parser specifically handles sudo command execution events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
