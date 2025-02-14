# Vector.dev Console Demo

This is a simple demonstration of Vector.dev using stdin as input and console as output.

## Prerequisites

- Vector.dev installed on your system
- Basic understanding of terminal/command line

## Configuration

The `vector.toml` configuration file sets up:
- A stdin source that accepts input from terminal
- A console sink that outputs the data to terminal

## Running the Demo

1. Start Vector with the configuration:
```bash
vector --config vector.toml
```

2. Type any text in the terminal and press Enter
   - The text will be processed by Vector and output to the console
   - Each line you type will be processed separately

3. To stop Vector, press Ctrl+C

## Example

```bash
$ vector --config vector.toml
hello world
hello world
this is a test
this is a test
```

The input text appears as output because we're using the console sink with text encoding.
