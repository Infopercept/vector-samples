# Extract Raw Syslog Demo

This demo shows how to generate and extract raw syslog messages using Vector.

## Prerequisites

- Vector installed on your system
- Basic understanding of Vector configuration

## Configuration

The `extract_raw_logs.toml` configuration file:
- Generates 100 demo syslog messages
- Writes them to a file named `raw_demo_syslog.log`

## Running the Demo

1. Navigate to the directory containing the configuration:
```bash
cd extract-raw-demo-syslogs
```

2. Run Vector with the configuration file:
```bash
vector --config extract_raw_logs.toml
```

3. Check the output:
```bash
cat raw_demo_syslog.log
```

The generated syslog messages will be written to `raw_demo_syslog.log` in raw text format.

## Configuration Details

- Source: Uses `demo_logs` type with syslog format
- Sink: Writes to a file with text encoding
- Count: Generates 10 sample messages
