# Ubuntu SSH Log Parser

A Vector.dev configuration for parsing and analyzing SSH log entries from Ubuntu's auth.log files.

## Overview

This tool helps system administrators monitor and analyze SSH access patterns by parsing auth.log files. It provides detailed insights into login attempts, potential security threats, and access patterns.

## Project Structure

```
Ubuntu-SSH-Log-Parser/
├── attempted_login/
│   ├── vector.yaml
│   ├── auth.log
│   ├── vector_parsed_log.json
│   └── README.md
├── sshd_accepted_password/
│   ├── vector.yaml
│   ├── auth.log
│   ├── vector_parsed_log.json
│   └── README.md
├── ssh_check_pass/
│   ├── vector.yaml
│   ├── auth.log
│   ├── vector_parsed_log.json
│   └── README.md
└── README.md
```

## Features

- Real-time SSH log monitoring and parsing
- Structured output in JSON format
- Support for multiple SSH event types:
  - Failed password attempts
  - Successful logins
  - User shell modifications
  - Invalid users
  - Connection closes

## Requirements

- Vector v0.44 or higher
- Access to Ubuntu auth.log files
- Write permissions for output directory

## Installation

1. Install Vector:
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.vector.dev | sh
```

2. Copy the relevant configuration to your Vector configuration directory

## Usage

### Basic Usage

Run Vector with the configuration:
```bash
vector --config vector.yaml
```

### Configuration Options

Each subdirectory contains specific configurations for different log parsing scenarios:

1. SSH Failed Password Attempts
2. SSH Accepted Password Logins
3. Usermod Shell Changes

## Output Format

The parser generates structured JSON output. Example:

```json
{
    "timestamp": "2023-11-15 10:30:45",
    "hostname": "ubuntu-server",
    "program": "sshd",
    "pid": 12345,
    "event_type": "ssh_failed_password",
    "username": "user123",
    "ip": "192.168.1.100"
}
```

## Testing

Test configurations using Vector's test command:
```bash
vector test --config your_config.yaml
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## License

MIT License
