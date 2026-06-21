# Linux Web Server Health Toolkit

A Linux support toolkit for diagnosing Apache and Nginx service health, configuration validity, ports, certificates, logs and local HTTP behaviour and applying selected guarded service repairs.

## Diagnostic script

```bash
chmod +x src/linux_web_server_health.sh
sudo ./src/linux_web_server_health.sh
```

Specify a hostname and HTTPS port:

```bash
sudo ./src/linux_web_server_health.sh --host example.com --https-port 443
```

The diagnostic script detects Apache or Nginx, captures service and socket state, tests configuration syntax, reviews virtual hosts, checks local HTTP responses, reports certificate expiry and summarises recent errors.

## Repair script

Preview the standard repair:

```bash
chmod +x src/linux_web_server_repair.sh
sudo ./src/linux_web_server_repair.sh --repair --dry-run
```

Back up configuration, validate it, enable the detected service, and reload it when active or start it when stopped:

```bash
sudo ./src/linux_web_server_repair.sh --repair
```

Choose a server explicitly and require an HTTP verification result:

```bash
sudo ./src/linux_web_server_repair.sh \
  --server nginx \
  --repair \
  --verify-url https://127.0.0.1
```

Run one explicit service action or the installed log-rotation policy:

```bash
sudo ./src/linux_web_server_repair.sh --service-action restart
sudo ./src/linux_web_server_repair.sh --rotate-logs
```

Supported service actions are `start`, `restart`, `reload`, `enable` and `reset-failed`. Use `--yes` for non-interactive confirmation and `--output DIR` to select the evidence directory.

## What the repair does

- Detects an installed Nginx, Debian-style Apache or RHEL-style HTTPD service.
- Supports explicit `auto`, `nginx` and `apache` selection.
- Requires root for real changes and returns a distinct privilege exit code.
- Creates a protected configuration archive before service repair actions.
- Runs `nginx -t`, `apache2ctl configtest`, `apachectl configtest` or `httpd -t` before changing service state.
- Skips service changes when configuration validation fails.
- Can enable, start, restart, reload or clear failed service state.
- Can run the server's installed `logrotate` policy.
- Captures before-and-after service, configuration-test, socket, disk and journal evidence.
- Can require a successful HTTP or HTTPS response with `--verify-url`.
- Supports dry-run, confirmation controls, action logs and clear exit codes.

## Safety and limitations

The repair does not edit web-server configuration, renew certificates, change firewall rules or modify website content. Service reloads and restarts can interrupt requests. Configuration backups may include private TLS key references or files depending on local layout and are created with restrictive permissions; protect and remove them according to your security policy.

## Requirements

- Bash 4+
- systemd
- Nginx or Apache HTTP Server
- `curl` only when `--verify-url` is used
- `logrotate` only when `--rotate-logs` is used
- Root privileges for actual repair actions

## Author

Dewald Pretorius — L2 IT Support Engineer
