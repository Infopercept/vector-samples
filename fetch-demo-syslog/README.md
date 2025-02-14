# Fetch and Parse Syslog Demo

This demo shows how to fetch raw syslog messages and parse them into structured JSON format using Vector.

## Prerequisites

- Vector installed on your system
- Raw syslog messages in `raw_demo_syslog.log` file (generated from extract-raw-demo-syslogs)
- Basic understanding of Vector configuration

## Configuration

The `fetch_demo_syslog.toml` configuration:
- Reads raw syslog messages from `raw_demo_syslog.log`
- Parses syslog messages into structured format
- Outputs parsed messages to `parsed_syslog.json`

## Running the Demo

1. Ensure you have generated raw syslog messages first:
```bash
cd ../extract-raw-demo-syslogs
vector --config extract_raw_logs.toml
```

2. Navigate to the fetch_demo_syslog directory:
```bash
cd ../fetch_demo_syslog
```

3. Run Vector with the configuration:
```bash
vector --config fetch_demo_syslog.toml
```

4. Check the parsed output:
```bash
cat parsed_syslog.json
```

The parsed syslog messages will be written to `parsed_syslog.json` in structured JSON format.

## Configuration Details

- Source: Reads from `raw_demo_syslog.log` file
- Transform: Parses syslog messages using VRL
- Sink: Writes structured data to JSON file
