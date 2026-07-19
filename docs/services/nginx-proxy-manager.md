# Nginx Proxy Manager

## Purpose

Nginx Proxy Manager provides a centralized reverse proxy for all internal web services.

## Admin Interface

| Service | URL |
|---------|-----|
| Nginx Proxy Manager | http://192.168.50.2:81 |

## Configured Proxy Hosts

| Service | Domain | Backend |
|---------|--------|---------|
| Homepage | http://homepage.home.lab | http://192.168.50.2:3000 |
| Portainer | https://portainer.home.lab | https://192.168.50.2:9443 |
| Uptime Kuma | http://status.home.lab | http://192.168.50.2:3001 |

## DNS

Configured with pfSense DNS Resolver Host Overrides.

## Issues Encountered

### Portainer

**Problem**

- 502 Bad Gateway

**Cause**

- Portainer uses HTTPS on port 9443.
- Self-signed certificate.

**Solution**

```nginx
proxy_ssl_verify off;
```

### Homepage

**Problem**

- Host validation failed

**Cause**

Homepage only allowed specific hostnames.

**Solution**

```yaml
HOMEPAGE_ALLOWED_HOSTS: "*"
```

## Result

Internal services are now accessible using friendly DNS names instead of IP addresses and ports.
