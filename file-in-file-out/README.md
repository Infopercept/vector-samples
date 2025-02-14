# Vector File-to-File Example

This example demonstrates how to use Vector to read from a file and write to another file.

## Prerequisites

- [Vector](https://vector.dev) installed on your system
- Basic understanding of TOML configuration

## Setup

1. Create the input file:
```bash
echo "This is a test log line" > sample-input.txt
```

2. Ensure your directory structure looks like this:
```
file-in-file-out/
├── vector.toml
├── sample-input.txt
└── README.md
```

## Configuration

The `vector.toml` file is configured to:
- Read from `sample-input.txt` in the current directory
- Write the output to `output.txt` in the current directory
- Start reading from the beginning of the file (`start_at_beginning = true`)

## Running Vector

To run Vector with this configuration:

```bash
vector --config vector.toml
```

## Verifying Output

After running Vector, you can check the contents of the output file:

```bash
cat output.txt
```

## Stopping Vector

To stop Vector, press `Ctrl+C` in your terminal.

## Troubleshooting

If you encounter issues:
1. Verify all files exist in the correct locations
2. Check file permissions
3. Ensure Vector is properly installed by running `vector --version`
