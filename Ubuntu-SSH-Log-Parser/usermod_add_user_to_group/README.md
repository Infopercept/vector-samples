# Usermod Add User to Group Parser

This Vector configuration parses events from system logs when the usermod command adds users to groups.

## Overview

The configuration detects and parses log entries when users are added to groups using usermod. It extracts relevant information such as timestamp, hostname, program details, and group modification details.

## Input Format

The parser expects syslog messages in the following format:

```
Nov 15 11:22:33 ubuntu-server usermod[1234]: add 'username' to group 'groupname'
```

Or for shadow groups:

```
Nov 15 11:22:33 ubuntu-server usermod[1234]: add 'username' to shadow group 'groupname'
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for usermod group addition events
2. Extract timestamp, hostname, and program information
3. Parse the username and group details
4. Identify shadow group additions
5. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_usermod.json` in the following format:

```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "usermod_add",
  "appname": "usermod_add",
  "pid": 1234,
  "entity": "username",
  "group": "groupname",
  "group_type": "normal group",
  "event_type": "usermod_add_user_to_group"
}
```

This JSON output provides a structured representation of user group modification events, making it easier to analyze and process the log data.

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

- The parser specifically handles usermod group addition events
- Distinguishes between normal groups and shadow groups
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
