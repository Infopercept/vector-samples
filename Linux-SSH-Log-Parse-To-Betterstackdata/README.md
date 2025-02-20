# Vector Configuration for Linux SSH Log Parsing

This Vector configuration file parses Linux SSH authentication logs and forwards them to BetterStack.

## Configuration Overview

### Sources
- Monitors `/var/log/secure` for authentication logs
- Reads from beginning of file
- Ignores existing checkpoints

### Transforms
Parses various SSH authentication events including:
- Failed password attempts
- Invalid user access 
- Successful logins
- User disconnections
- Session opens/closes
- Sudo commands
- Authentication failures

### Sink 
- Forwards parsed logs to BetterStack via HTTP POST
- Uses JSON encoding
- Requires bearer token authentication

## Installation & Usage

1. Update the BetterStack URI and token in the `sinks` section
2. Place file at `/etc/vector/vector.yaml`
3. Validate the configuration:
```bash
vector validate 
```
4. Run vector.yaml file:
```bash
vector --config-yaml /etc/vector/vector.yaml
```

```

## Troubleshooting

If you encounter issues:
1. Check Vector logs for errors:
```bash
sudo journalctl -u vector -f
```
2. Verify file permissions:
```bash
sudo chown -R vector:vector /etc/vector/
sudo chmod 644 /etc/vector/vector.yaml
```
3. Ensure source log file is readable by Vector