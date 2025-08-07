# Surge Modules

Collection of Surge modules for Mac - VPN integrations and custom configurations.

## SealSuite VPN Integration Module

This module configures Surge to work properly with SealSuite VPN using multiple exclusion methods: domain-based proxy skipping, IP-based rejection rules, and process-based routing rules.

📊 **[View Integration Flow Diagram](docs/sealsuite-surge-integration-flow.md)** - Visual guide showing how SealSuite VPN and Surge work together

### Features

- Skip proxy for Claude AI, Anthropic, and Docker Hub domains
- Block Claude AI and Anthropic domains and IP addresses with rejection rules
- Direct routing for 30.100.0.0/16 subnet (bypasses VPN for internal network access)
- Direct routing for corplink-service process traffic
- Multi-layer protection for comprehensive VPN integration
- Ensures proper functionality when using SealSuite VPN alongside Surge
- Easy URL-based installation and updates

### Installation

#### Method 1: Install from URL (Recommended)

1. Open **Surge for Mac**
2. Navigate to the **Module** section (More → Module)
   
   ![Navigate to Module](images/surge-module-navigation.png)

3. Click **Install from URL...**
   
   ![Install from URL button](images/surge-install-from-url.png)

4. Paste the following URL:
   ```
   https://raw.githubusercontent.com/Liu-huaicheng/surge-modules/main/sealsuite-vpn.sgmodule
   ```
   
   ![Enter URL dialog](images/surge-enter-url.png)

5. Click **Done** to install the module

6. Enable the module by checking the **Enabled** checkbox
   
   ![Enable module](images/surge-module-enabled.png)

7. Click **Apply** to save changes

#### Method 2: Manual Installation

1. Download the `sealsuite-vpn.sgmodule` file
2. Open **Surge for Mac**
3. Go to the **Modules** tab
4. Click **Install Module from File**
5. Select the downloaded file

### Updating the Module

To update the module to get the latest changes:

1. Open **Surge for Mac**
2. Navigate to the **Module** section (More → Module)
3. Find the **SealSuite VPN Integration** module
4. Right-click on the module to show the context menu
5. Select **Update...** from the menu
   
   ![Update module context menu](images/surge-module-update.png)

6. The module will automatically fetch and apply the latest version
7. Click **Apply** to save changes

> **💡 Tip**: You can also use **Copy URL** from the context menu to share the module URL with others, or **Delete...** to remove the module if needed.

### What This Module Does

The module adds multi-layer exclusions to your Surge setup:

```ini
#!name=SealSuite VPN Integration
#!desc=Enable SealSuite VPN to work alongside Surge with domain exclusions, IP exclusions, and process rules
#!system=mac
#!category=VPN

[General]
# Skip proxy for Claude AI, Anthropic, and Docker Hub domains
skip-proxy = %APPEND% *.claude.ai, *.anthropic.com, claude.ai, anthropic.com, *.docker.io, docker.io


[Rule]
# Reject Claude AI and Anthropic domains and IP addresses
DOMAIN-SUFFIX,claude.ai,REJECT,extended-matching
DOMAIN-SUFFIX,anthropic.com,REJECT,extended-matching
IP-CIDR,160.79.104.10/32,REJECT

# Direct connection for 30.100.0.0/16 subnet (bypass VPN)
IP-CIDR,30.100.0.0/16,DIRECT

# Direct connection for corplink-service process
PROCESS-NAME,corplink-service,DIRECT
```

This configuration provides comprehensive protection:

- **Domain-based exclusion** (`skip-proxy`): Handles domain resolution and works with Surge's proxy server
- **Domain suffix rejection** (`DOMAIN-SUFFIX`): Completely blocks access to Claude AI and Anthropic domains with extended matching for comprehensive coverage
- **IP address rejection** (`IP-CIDR`): Blocks specific IP addresses associated with Claude AI and Anthropic services
- **Subnet-based direct routing** (`IP-CIDR` with DIRECT): Routes traffic to the 30.100.0.0/16 subnet directly, bypassing VPN for internal network access
- **Process-based routing** (`PROCESS-NAME`): Routes traffic from specific processes (corplink-service) directly without proxy

All configurations work together to ensure that traffic to Claude AI, Anthropic, and Docker Hub services, plus internal network traffic (30.100.x.x) and corplink-service process traffic, goes directly through your SealSuite VPN connection without interference from Surge's routing.

> **📝 Important Note**: Some network requests may bypass Surge entirely due to SealSuite VPN's built-in DNS server and intelligent routing. SealSuite DNS classifies domains and can redirect corporate/internal traffic through VPN tunnels before Surge processes them. This module ensures that excluded services (Claude AI, Anthropic, Docker Hub, corplink-service) work optimally in this mixed routing environment.

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