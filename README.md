# Surge Modules

Collection of Surge modules for Mac - VPN integrations and custom configurations.

## SealSuite VPN Integration Module

This module configures Surge to work properly with SealSuite VPN using dual-layer exclusions: domain-based proxy skipping and IP-based TUN interface exclusions.

### Features

- Skip proxy for Claude AI and Anthropic domains
- Exclude Claude AI and Anthropic IP addresses from TUN interface routing
- Dual-layer protection for comprehensive VPN integration
- Ensures proper functionality when using SealSuite VPN alongside Surge
- Easy URL-based installation

### Installation

#### Method 1: Install from URL (Recommended)

1. Open **Surge for Mac**
2. Go to the **Modules** tab
3. Click **Install Module from URL**
4. Paste the following URL:
   ```
   https://raw.githubusercontent.com/Liu-huaicheng/surge-modules/main/sealsuite-vpn.sgmodule
   ```
5. Click **Install**

#### Method 2: Manual Installation

1. Download the `sealsuite-vpn.sgmodule` file
2. Open **Surge for Mac**
3. Go to the **Modules** tab
4. Click **Install Module from File**
5. Select the downloaded file

### What This Module Does

The module adds dual-layer exclusions to your Surge setup:

```ini
[General]
# Skip proxy for Claude AI and Anthropic domains
skip-proxy = %APPEND% *.claude.ai, *.anthropic.com, claude.ai, anthropic.com

# Exclude Claude AI and Anthropic IP addresses from TUN interface
tun-excluded-routes = %APPEND% 160.79.104.10/32
```

This configuration provides comprehensive protection:

- **Domain-based exclusion** (`skip-proxy`): Handles domain resolution and works with Surge's proxy server
- **IP-based exclusion** (`tun-excluded-routes`): Excludes specific IP addresses from TUN interface routing, ensuring traffic bypasses the VPN tunnel entirely

Both configurations work together to ensure that traffic to Claude AI and Anthropic services goes directly through your SealSuite VPN connection without interference from Surge's routing.

### Compatibility

- **Platform**: macOS only
- **Surge Version**: Compatible with Surge for Mac
- **SealSuite VPN**: Works with all SealSuite VPN configurations

### Support

If you encounter any issues:

1. Make sure both Surge and SealSuite VPN are properly configured
2. Check that the module is enabled in Surge's Modules tab
3. Restart Surge after installing the module

### License

This module is provided as-is for educational and personal use.