# Linux Web Server Health Toolkit

A read-only Bash toolkit for diagnosing Apache and Nginx service health, configuration validity, ports, certificates, logs, and local HTTP response behaviour.

## Features

- Detects Apache HTTP Server and Nginx installations
- Captures service state, enablement, process, and socket evidence
- Runs safe configuration syntax tests
- Reviews virtual-host or server-block configuration
- Checks local HTTP and HTTPS response headers
- Reports certificate subject, issuer, expiry, and remaining days
- Summarises recent error-log entries
- Captures CPU, memory, and disk context relevant to web-service incidents
- Produces text and JSON reports

## Usage

```bash
chmod +x src/linux_web_server_health.sh
sudo ./src/linux_web_server_health.sh
```

Specify a hostname and port:

```bash
sudo ./src/linux_web_server_health.sh --host example.com --https-port 443
```

## Safety

The script does not reload services, modify configuration, renew certificates, change firewall rules, or edit websites.

## Validation

Test with Nginx, Apache, an expired lab certificate, an invalid configuration file, and a stopped service.

## Author

Dewald Pretorius — L2 IT Support Engineer
