# User and Group Addition Parser

This Vector configuration parses user and group addition events from authentication logs, tracking system user management activities.

## Overview

The configuration detects and parses log entries when new users or groups are added to the system. It extracts relevant information such as timestamp, hostname, and user/group details.

## Input Format

The parser expects syslog messages in the following formats:

For new users:
```
Nov 15 11:22:33 ubuntu-server useradd[1234]: new user: name=johndoe, UID=1001, GID=1001, home=/home/johndoe, shell=/bin/bash, from=/etc/adduser.conf
```

For new groups:
```
Nov 15 11:22:33 ubuntu-server groupadd[1234]: new group: name=developers, GID=1001
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the syslog pattern for both user and group addition events
2. Extract timestamp, hostname, and process information
3. Parse specific details like UID, GID, home directory, and shell for users
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entries will be written to `vector_parsed_useradd.json` in the following formats:

For new users:
```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "useradd",
  "appname": "useradd",
  "pid": 1234,
  "log_type": "new user",
  "name": "johndoe",
  "uid": 1001,
  "gid": 1001,
  "home": "/home/johndoe",
  "shell": "/bin/bash",
  "from": "/etc/adduser.conf",
  "event_type": "useradd_event"
}
```

For new groups:
```json
{
  "timestamp": "Nov 15 11:22:33",
  "hostname": "ubuntu-server",
  "program": "groupadd",
  "appname": "groupadd",
  "pid": 1234,
  "log_type": "new group",
  "name": "developers",
  "gid": 1001,
  "event_type": "useradd_event"
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

- The parser handles both user and group addition events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
