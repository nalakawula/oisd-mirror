# Blocky DNS Server with OISD Block Lists

A DNS server configuration using [Blocky](https://github.com/0xERR0R/blocky) with OISD (One Internet, Safe Domain) block lists for ad blocking and content filtering.

## Overview

This project provides a ready-to-use Blocky DNS server configuration that:
- Blocks ads, nsfw and malicious domains using OISD block lists
- Forwards DNS queries to secure DNS-over-HTTPS (DoH) servers
- Provides local DNS resolution for custom domains
- Includes Prometheus metrics for monitoring

## Features

- **Ad Blocking**: Uses OISD big list for comprehensive ad and tracker blocking
- **NSFW Filtering**: Optional NSFW content blocking using OISD NSFW list
- **DoH Support**: Secure DNS queries via DNS-over-HTTPS
- **Local DNS**: Custom DNS mappings for internal services
- **Monitoring**: Built-in Prometheus metrics
- **Auto-refresh**: Block lists update every 24 hours

## Configuration

The DNS server is configured to:
- Listen on port 53 for DNS queries
- Serve web interface on port 8080
- Use AdGuardHome's public DoH servers as upstream resolvers
- Block domains from both local files and remote OISD mirrors

### Upstream DNS Servers
- Primary: AdGuardHome (94.140.14.140, 94.140.14.141)
- Fallback: Cloudflare (1.1.1.1), Quad9 (9.9.9.10, 149.112.112.10)

## OISD Mirror Usage

Due to accessibility issues with the original OISD endpoints, this configuration uses:
- **Mirror Repository**: [nalakawula/oisd-mirror](https://github.com/nalakawula/oisd-mirror)
- **Local Files**: Backup copies stored locally (`oisd_big`, `oisd_nsfw`). To ensure we still have dns deny list if remote endpoint inaccessible.

### Why Use Mirrors?

The original OISD endpoints (`https://big.oisd.nl/domainswild` and `https://nsfw.oisd.nl/domainswild`) may be inaccessible from certain networks or regions. This setup provides redundancy by using both GitHub mirrors and local file backups.

## Quick Start

1. Ensure you have [Blocky](https://github.com/0xERR0R/blocky) installed
2. Clone this repository
3. Update the local file paths in `config.yml` to match your setup
4. Run Blocky with the provided configuration:
   ```bash
   blocky --config config.yml
   ```

## Files

- `config.yml`: Main Blocky configuration file
- `oisd_big`: Local copy of OISD big block list
- `oisd_nsfw`: Local copy of OISD NSFW block list

## Acknowledgments

- **[Blocky](https://github.com/0xERR0R/blocky)**: Fast and lightweight DNS proxy with ad-blocking capabilities
- **[AdGuardHome](https://adguard.com/en/adguard-home/overview.html)**: Public DoH servers
- **[OISD](https://oisd.nl/)**: Comprehensive domain block lists for ad, nsfw, and malware blocking