# Surge Modules

Collection of Surge modules for Mac - VPN integrations and custom configurations.

## SealSuite VPN Integration Module

This module configures Surge to work properly with SealSuite VPN by skipping proxy for specific domains.

### Features

- Skip proxy for Claude AI and Anthropic domains
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

The module adds the following configuration to your Surge setup:

```ini
[General]
skip-proxy = %APPEND% *.claude.ai, *.anthropic.com, claude.ai, anthropic.com
```

This ensures that traffic to Claude AI and Anthropic services bypasses Surge's proxy and goes directly through your SealSuite VPN connection.

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