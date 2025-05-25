# Tor Proxy for Runtipi

This app provides a Tor SOCKS proxy that can be used to route traffic through the Tor network for enhanced privacy and anonymity.

## Features

- SOCKS5 proxy on port 9050
- Tor control port on 9051 for advanced configuration
- Persistent data storage
- Compatible with SearXNG and other privacy-focused applications

## Usage with SearXNG

To use this Tor proxy with SearXNG, configure your SearXNG instance with the following proxy settings:

```yaml
outgoing:
  proxies:
    all://:
      - socks5://tor:9050
```

Replace `tor` with the actual hostname or IP address of your Tor container if needed.

## Network Configuration

- **SOCKS Proxy Port**: 9050
- **Control Port**: 9051

## Security Notes

- This proxy provides anonymity for outgoing connections
- Always verify your Tor connection is working properly
- Be aware of the limitations and potential risks of using Tor
- Some services may block Tor exit nodes

## Additional Configuration

You can provide custom Tor configuration through the `TOR_CONFIG` environment variable in the app settings.
