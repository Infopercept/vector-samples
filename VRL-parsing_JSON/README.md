# VRL JSON Parsing Example

This example demonstrates how to parse and transform JSON data using Vector Remap Language (VRL).

## Files

- `input.json` - Contains a JSON message with a nested JSON string
- `program.vrl` - VRL script that processes the JSON data
- `output.json` - Expected output after transformation

## What the Program Does

The VRL script performs the following operations:

1. Parses the nested JSON string from the message field
2. Handles timestamp parsing and formatting:
   - Attempts to parse the timestamp using ISO 8601 format
   - Falls back to current timestamp if parsing fails
   - Adds a formatted timestamp string
3. Removes the username field
4. Converts the message field to lowercase

## Example Input

```json
{"message": "{\"status\":200,\"timestamp\":\"2021-03-01T19:19:24.646170Z\",\"message\":\"SUCCESS\",\"username\":\"ub40fan4life\"}"}
```

## Example Output

```json
{ "message": "success", "status": 200, "timestamp": 1614606564, "timestamp_str": "2021-03-01T13:49:24Z" }
```

## Running the Example

You can run this example using Vector's VRL CLI tool:

```bash
vector vrl --input input.json --program program.vrl --print-object > output.json
```
