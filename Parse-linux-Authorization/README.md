# Parse Linux Authorization Logs

This directory demonstrates how to parse Linux SSH authorization logs using Vector.dev.

## Overview

This configuration reads SSH authorization logs, parses them into a structured format, and outputs them as JSON. It's useful for monitoring SSH login attempts and access patterns.

## Directory Structure

```
Parse-linux-Authorization/
├── ssh.log           # Sample SSH log file
├── vector.toml       # Vector configuration
├── vector_parsed_log.json  # Output file
└── README.md         # This file
```

## Configuration

The `vector.toml` configuration performs three main operations:

1. **Source**: Reads SSH logs from the specified file
2. **Transform**: Parses logs using the `parse_linux_authorization` VRL function
3. **Sink**: Outputs structured JSON to a file

## Sample Input/Output

### Input (ssh.log):
```log
Mar 23 01:49:58 localhost sshd[1111]: Accepted publickey for eng from 10.1.1.1 port 8888 ssh2: RSA SHA256:foobar
```

### Output (vector_parsed_log.json):
```json
{
  "appname": "sshd",
  "hostname": "localhost",
  "message": "Accepted publickey for eng from 10.1.1.1 port 8888 ssh2: RSA SHA256:foobar",
  "procid": 1111,
  "timestamp": "2025-03-22T20:19:58Z"
}
```

## Usage

1. Ensure Vector is installed on your system:
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.vector.dev | sh
```

2. Run Vector with the configuration:
```bash
vector --config vector.toml
```

## Configuration Details

### Source Configuration
- Type: `file`
- Reads from: `ssh.log`
- Starts from beginning of file

### Transform Configuration
- Type: `remap`
- Uses: `parse_linux_authorization` VRL function
- Parses standard Linux authorization log format

### Sink Configuration
- Type: `file`
- Output format: JSON
- Destination: `vector_parsed_log.json`

## Parsed Fields

The parser extracts these fields from SSH logs:
- `appname`: Application name (e.g., sshd)
- `hostname`: System hostname
- `message`: Complete log message
- `procid`: Process ID
- `timestamp`: ISO 8601 formatted timestamp

## Troubleshooting

1. Verify file permissions:
```bash
ls -l ssh.log vector_parsed_log.json
```

2. Check Vector logs:
```bash
vector validate vector.toml
```

3. Ensure correct file paths in `vector.toml`

## Additional Resources

- [Vector Documentation](https://vector.dev/docs/)
- [VRL Function Reference](https://vector.dev/docs/reference/vrl/)
- [Linux Authorization Logs Format](https://www.gnu.org/software/libc/manual/html_node/syslog.html)