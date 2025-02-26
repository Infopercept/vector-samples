# Attempted Login Parser Configuration

This Vector configuration parses attempted login events from Ubuntu authentication logs.

## Overview

The configuration detects and parses log entries for login attempts from auth.log files. It extracts relevant information such as timestamp, hostname, program details, and user information.

## Input Format

The parser expects authentication log messages in the following format:

```
Oct 15 14:30:45 myhost login: Attempted login by user123 (UID: 1000) on tty1
```

## Configuration Details

The configuration uses Vector's parsing capabilities to:
1. Match the authentication log pattern for login attempt events
2. Extract timestamp, hostname, and program information
3. Parse the username, UID, and TTY details
4. Structure the data into a standardized JSON format

### Sample Output

The parsed log entry will be written to `vector_parsed_nologin.json` in the following format:

```json
{
  "timestamp": "Oct 15 14:30:45",
  "hostname": "myhost",
  "program": "login",
  "username": "user123",
  "user_uid": 1000,
  "tty": "tty1",
  "event_type": "attempted_login"
}
```

This JSON output provides a structured representation of login attempt events, making it easier to analyze and process the log data.

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

- The parser specifically handles login attempt events
- Make sure your log format matches the expected input format
- Adjust file paths in the configuration according to your system
