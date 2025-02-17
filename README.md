# Vector.dev Demonstrations

This repository contains various demonstrations of Vector.dev configurations for different use cases.

## Projects

### 1. Console Input/Output Demo (console-in-console-out)
A basic demonstration showing Vector's console-to-console data pipeline.

#### Usage
```bash
vector --config console-in-console-out/vector.toml
```
- Type messages in the console
- See the processed output immediately

### 2. Raw Demo Syslog Extractor (extract-raw-demo-syslog)
Extracts and processes raw syslog messages from demo data.

#### Features
- Reads demo syslog data
- Parses and structures the messages
- Outputs to specified format

### 3. Demo Syslog Fetcher (fetch-demo-syslog)
Fetches and processes demo syslog messages with enhanced parsing.

#### Key Components
- Syslog message extraction
- Advanced parsing rules
- Structured output generation

### 4. System Syslog Parser (fetch-system-syslogs)
Production-ready system syslog parsing configuration.

#### Features
- Real-time system log monitoring
- Structured parsing of syslog messages
- JSON output format
- Handles various syslog formats

### 5. File Input/Output Demo (file-in-file-out)
Demonstrates file-based input and output operations.

#### Usage
```bash
vector --config file-in-file-out/vector.toml
```
- Reads from input file
- Processes data
- Writes to output file

### 6. VRL JSON Parsing (VRL-parsing_JSON)
Demonstrates parsing and transforming nested JSON data using VRL.

#### Features
- Parses nested JSON strings
- Handles timestamp parsing and formatting
- Field transformations and removal
- Case conversion

#### Example Usage
```bash
vector vrl --input input.json --program program.vrl --print-object > output.json
```

### 7. VRL Transformation (VRL_transformation)
Shows basic data transformation capabilities using VRL.

#### Features
- Field removal and addition
- Timestamp generation
- HTTP status code parsing
- Status field mapping

#### Example Usage
```bash
vector --config vector.toml
```

## Repository Structure
```
learning-vector.dev/
├── console-in-console-out/
│   └── vector.toml
├── extract-raw-demo-syslog/
│   └── vector.toml
├── fetch-demo-syslog/
│   └── vector.toml
├── fetch-system-syslogs/
│   ├── vector.toml
│   └── README.md
├── file-in-file-out/
│   └── vector.toml
├── VRL-parsing_JSON/
│   ├── input.json
│   ├── program.vrl
│   ├── output.json
│   └── README.md
├── VRL_transformation/
│   ├── input.json
│   ├── program.vrl
│   ├── output.json
│   └── README.md
└── README.md
```

## Prerequisites
- Vector.dev installed on your system
- Basic understanding of data processing pipelines
- Access to system logs (for syslog demos)
- Read/write permissions for file operations

## Getting Started

1. Clone this repository
2. Install Vector if not already installed:
   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.vector.dev | sh
   ```
3. Navigate to the desired example directory
4. Run the specific configuration using:
   ```bash
   vector --config <configuration-file>.toml
   ```

### Running VRL Examples

For VRL-specific examples, you can use either of these methods:

1. Using VRL CLI tool:
   ```bash
   vector vrl --input input.json --program program.vrl --print-object > output.json
   ```

2. Using Vector configuration:
   ```bash
   vector --config vector.toml
   ```

## Configuration Details

Each directory contains:
- A Vector configuration file (`.toml`)
- Sample data files (where applicable)
- Specific README with detailed instructions (where applicable)

## Common Use Cases

1. **Console Demo**: Testing and learning Vector basics
2. **Raw Syslog**: Processing basic syslog data
3. **Demo Syslog**: Advanced syslog parsing
4. **System Syslog**: Production system monitoring
5. **File Operations**: Batch data processing
6. **VRL JSON Parsing**: Complex JSON transformation and nested JSON handling
7. **VRL Basic Transformation**: Field manipulation and status code mapping

For more information about Vector, visit [vector.dev](https://vector.dev)

## Troubleshooting

- Check file permissions
- Verify Vector installation
- Ensure correct configuration paths
- Review Vector logs for errors
