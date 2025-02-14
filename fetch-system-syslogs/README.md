# System Syslog Parser with Vector

This configuration demonstrates how to parse system syslog messages using Vector.

## Prerequisites

- Vector installed on your system
- Access to system syslog files

## Configuration

The `fetch_syslog.toml` configuration does the following:
1. Reads raw syslog messages from `raw_syslog.log`
2. Parses the syslog messages into structured data
3. Outputs the parsed data to `vector_parsed_syslog.json`

## Usage

1. First, make sure you have your syslog data in `raw_syslog.log`. You can create this by copying your system logs:
   ```bash
   sudo cp /var/log/syslog raw_syslog.log
   ```

2. Run Vector with the configuration:
   ```bash
   vector --config fetch_syslog.toml
   ```

3. The parsed output will be written to `vector_parsed_syslog.json`

## Output Format

The parsed syslog messages will be in JSON format with structured fields like:
- timestamp
- facility
- severity
- hostname
- message
- process_name
- pid (if available)

## Troubleshooting

If you encounter permission issues:
- Ensure Vector has read access to the input file
- Ensure Vector has write permissions for the output directory
