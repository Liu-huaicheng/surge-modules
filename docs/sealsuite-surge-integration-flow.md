# SealSuite VPN & Surge Integration Flow

Visual guide showing how network requests are handled when using SealSuite VPN alongside Surge for Mac.

## Network Request Flow Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#F4F4F5', 'primaryTextColor': '#18181B', 'primaryBorderColor': '#E4E4E7', 'lineColor': '#71717A', 'secondaryColor': '#F4F4F5', 'tertiaryColor': '#E4E4E7'}}}%%
graph LR
    subgraph Client Zone
        direction LR
        A["💻<br>Client App"]
    end

    subgraph System & Proxy Zone
        direction TB
        subgraph System Logic
            direction LR
            B{Respects<br>System Proxy?}
        end
        subgraph DNS & Routing Path
            direction TB
            C["🛡️<br>SealSuite DNS"] --> D{Foreign<br>Domain?}
            D -- No --> F{Surge<br>Enhanced Mode?}
            D -- Yes --> E["🔀<br>Respond with<br>Fake IP"]
            E --> J["🗺️<br>Adds Route to<br>System Table"]
        end
        subgraph Proxy Path
             direction TB
             G["⚡️<br>Surge Proxy"]
        end
    end

    subgraph Destination
        direction TB
        H["🖥️<br>Target Server"]
        I["🌐<br>External DNS"]
        K["🔒<br>Remote VPN<br>Server"]
    end

    A -- Request --> B

    B -- Yes --> G
    G -- "Handles All Traffic" --> H

    B -- No --> C
    
    J -- "Traffic rerouted" --> K
    K -- "Secure Tunnel" --> H
    
    F -- "Yes (Hijacks DNS)" --> G
    F -- "No (Direct DNS)" --> I
    I -- "Resolves DNS for" --> H
    
    classDef client fill:#A7F3D0,stroke:#15803D,stroke-width:2px,color:#18181B
    classDef system fill:#BFDBFE,stroke:#2563EB,stroke-width:2px,color:#18181B
    classDef destination fill:#FBCFE8,stroke:#9D2667,stroke-width:2px,color:#18181B
    classDef decision fill:#FEF08A,stroke:#A16207,stroke-width:2px,color:#18181B

    class A client
    class C,E,G,J system
    class H,I,K destination
    class B,D,F decision
```

## Flow Components Explained

### Client Zone
- **💻 Client App**: Any application on the user's device making network requests

### System & Proxy Zone
- **🛡️ SealSuite DNS**: Built-in DNS server that intelligently classifies domains
- **⚡️ Surge Proxy**: Surge for Mac handling proxy requests when system proxy is enabled
- **🔀 Fake IP Response**: SealSuite returns fake IPs for foreign domains to trigger routing
- **🗺️ System Route Table**: OS-level routing rules added by SealSuite

### Destination
- **🖥️ Target Server**: Final destination server (corporate or external)
- **🌐 External DNS**: Public DNS servers for domain resolution
- **🔒 Remote VPN Server**: SealSuite VPN gateway for secure corporate access

## Request Flow Process

1. **Initial Request**: Client app initiates a network request
2. **System Proxy Check**: System determines if the request should go through configured proxy
3. **DNS Classification**: SealSuite DNS analyzes the domain:
   - **Corporate domains**: Classified as "non-foreign" → routed through VPN tunnel
   - **External domains**: Classified as "foreign" → handled based on configuration
4. **Routing Decision**: Based on domain classification and Surge configuration:
   - **VPN Path**: Corporate resources → secure tunnel to VPN server
   - **Proxy Path**: External resources → through Surge proxy (if enhanced mode enabled)
   - **Direct Path**: External resources → direct DNS resolution (if enhanced mode disabled)

## Integration Benefits

- **🎯 Intelligent Routing**: Automatic classification and routing based on domain type
- **🔒 Security**: Corporate resources always go through secure VPN tunnel
- **⚡ Performance**: External traffic can be optimized through Surge
- **🔄 Seamless Integration**: No manual configuration needed for most scenarios
- **🛡️ DNS Protection**: Built-in DNS prevents leaks and ensures proper routing

## Module Configuration Impact

The SealSuite VPN Integration module ensures:
- Claude AI and Anthropic domains bypass Surge processing
- Corporate traffic (corplink-service) routes directly through VPN
- IP-based exclusions prevent TUN interface conflicts
- Multi-layer protection maintains optimal performance