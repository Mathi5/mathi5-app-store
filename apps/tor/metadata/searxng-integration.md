# SearXNG Integration Guide

This guide explains how to integrate the Tor proxy with your SearXNG instance.

## Method 1: Global Proxy Configuration

Add the following to your SearXNG `settings.yml`:

```yaml
outgoing:
  # Request timeout
  request_timeout: 10.0
  
  # Tor proxy configuration
  proxies:
    all://:
      - socks5://tor_tor_1:9050  # Replace with your Tor container name
      - socks5://localhost:9050  # Fallback if using host network
```

## Method 2: Engine-Specific Proxy

Configure only specific engines to use Tor:

```yaml
engines:
  - name: google
    proxies:
      all://:
        - socks5://tor_tor_1:9050
        
  - name: duckduckgo
    proxies:
      all://:
        - socks5://tor_tor_1:9050
```

## Method 3: Using Tor DNS

To also route DNS queries through Tor:

```yaml
outgoing:
  proxies:
    all://:
      - socks5://tor_tor_1:9050
  
  # Use Tor's DNS resolver
  dns_resolver: tor_tor_1:9053
```

## Testing the Connection

1. Check if Tor is running:
   ```bash
   curl --socks5 localhost:9050 https://check.torproject.org/api/ip
   ```

2. In SearXNG, search for "what is my ip" to verify you're using Tor exit nodes.

## Troubleshooting

- **Connection timeouts**: Increase `request_timeout` in SearXNG settings
- **Slow searches**: This is normal when using Tor due to the onion routing
- **Blocked searches**: Some search engines block Tor exit nodes
- **Container name**: Use `docker ps` to find the exact Tor container name

## Security Considerations

- Tor provides anonymity but not end-to-end encryption
- Some search engines may present more CAPTCHAs when using Tor
- Consider using `.onion` versions of search engines when available
