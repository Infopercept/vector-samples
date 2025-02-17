# VRL Transformation Example

This example demonstrates how to use Vector Remap Language (VRL) to transform JSON data.

## Files

- `input.json` - Contains the input data with fields to be transformed
- `program.vrl` - Contains the VRL transformation logic
- `output.json` - Shows the expected output after transformation

## Transformation Steps

1. Removes the `foo` field from the input
2. Generates a timestamp in ISO 8601 format
3. Parses the HTTP status code
4. Adds a `status` field based on the HTTP status code:
   - "success" for codes 200-299
   - "error" for all other codes

## Usage

Run this transformation using Vector:

```bash
vector --config vector.toml
```

## Example Input/Output

Input:
```json
{
  "message": "Hello VRL",
  "foo": "delete me",
  "http_status": "200"
}
```

Output:
```json
{
  "message": "Hello VRL",
  "status": "success",
  "timestamp": "2025-02-17T11:36:41Z"
}
```
