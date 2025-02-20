# Vector SSH Log Parser

A Vector configuration for parsing SSH authentication logs into structured OCSF format.

## Overview

This project demonstrates parsing SSH authentication logs using Vector and transforming them into the Open Cybersecurity Schema Framework (OCSF) format for better analysis and integration.

## Project Structure

```
SSH-Parsing/
├── vector.toml      # Vector configuration
├── ssh.log          # Input SSH log file
└── vector_parsed_log.json  # Output parsed JSON
```

## Configuration

The Vector pipeline consists of:

1. **Source**: Reads SSH authentication logs from `ssh.log`
2. **Transform**: 
   - Parses log messages using regex
   - Extracts authentication details
   - Maps to OCSF schema
3. **Sink**: Outputs structured JSON to `vector_parsed_log.json`

## Sample Output

```json
{
  "authentication": {
    "fingerprint": "SHA256:foobar",
    "key_type": "RSA",
    "method": "publickey"
  },
  "destination": {
    "hostname": "localhost"
  },
  "event": {
    "action": "login",
    "category": "authentication",
    "outcome": "success",
    "timestamp": "2025-03-22T20:19:58Z",
    "type": "user_login"
  },
  "source": {
    "ip": "10.1.1.1",
    "port": 8888
  }
}
```

## Usage

1. Ensure Vector is installed
2. Place your SSH logs in `ssh.log`
3. Run Vector:
   ```bash
   vector --config vector.toml
   ```

## Extracted Fields

- Authentication method and key details
- User information
- Source IP and port
- Protocol details
- Event timestamp and outcome
- Process information

## Requirements

- Vector data pipeline tool
- Read access to SSH log files
- Write permissions for output directory