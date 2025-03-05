# Ubuntu SSH Combined Log Parser

A Vector configuration for parsing Ubuntu SSH and authentication-related log messages.

## Overview

This configuration uses Vector to parse various SSH and authentication-related log messages from Ubuntu systems. It supports parsing multiple log patterns including login attempts, connections, disconnections, session management, and user/group modifications.

## Supported Event Types

### SSH Authentication Events
1. `attempted_login` - Login attempts with UID and TTY details
2. `sshd_accepted_password` - Successful password authentication events 
3. `sshd_authentication_failure` - General authentication failures
4. `sshd_check_pass` - Password check events
5. `sshd_failed_password` - Failed password authentication attempts
6. `sshd_failed_password_repeated` - Multiple failed password attempts
7. `sshd_invalid_user` - Invalid user login attempts

### SSH Connection Events
8. `sshd_connection_closed` - Connection closure events
9. `sshd_connection_reset` - Connection reset events
10. `sshd_disconnect` - Client disconnect events
11. `sshd_recieved_disconnect` - Server received disconnect events
12. `sshd_server_listening_IPv4` - IPv4 listening events
13. `sshd_server_listening_IPv6` - IPv6 listening events
14. `sshd_terminating` - SSH daemon termination events

### Session Management
15. `sshd_session_closed` - SSH session closure events
16. `sshd_session_opened` - SSH session creation events
17. `systemd_new_session` - New systemd session events
18. `systemd_session_logged_out` - Session logout events
19. `systemd_session_opened` - Systemd session opened events
20. `systemd_session_removed` - Session removal events

### PAM Authentication
21. `sshd_pam_authentication_failure` - PAM-specific authentication failures

### Sudo Events
22. `sudo_command_executed` - Sudo command execution tracking
23. `sudo_session_closed` - Sudo session closure events
24. `sudo_session_opened` - Sudo session creation events

### User Management
25. `useradd_new_user_group` - New user/group creation events
26. `usermod_add_user_to_group` - Group membership modifications
27. `usermod_change_user_shell` - User shell change events

## Common Fields

All parsed events include these standard fields:
- `timestamp` - Event timestamp
- `hostname` - System hostname
- `program` - Source program name
- `appname` - Application identifier
- `pid` - Process ID

## Event-Specific Fields

Events may include additional fields based on type:
- User Information: `username`, `uid`, `target_user`, `target_uid`
- Network Details: `source_ip`, `port`, `protocol`
- Session Info: `session_id`, `tty`
- Authentication: `pam_module`, `pam_activity`
- Command Details: `command`, `pwd` (for sudo events)
- Group Management: `group`, `group_type`

## Configuration

### Requirements
- Vector v0.44+
- Read access to auth.log files
- Write permissions for output directory

### Setup
1. Place `vector.yaml` in Vector configuration directory
2. Ensure Vector has auth.log access
3. Configure output path as needed
4. Start Vector service

## Output Format

Example output:
```json
{
  "timestamp": "Feb 20 10:41:42",
  "hostname": "ubuntu-server",
  "program": "sshd",
  "appname": "sshd",
  "pid": 3087,
  "event_type": "sshd_accepted_password",
  "username": "user123",
  "source_ip": "192.168.1.100",
  "port": 62721,
  "protocol": "ssh2"
}
```

## Error Handling
- Unmatched patterns are marked as `event_type: "unknown"`
- Parse failures are logged at debug level
- Invalid field values are handled gracefully
