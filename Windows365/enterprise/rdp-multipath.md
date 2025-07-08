---
# Required metadata
# For more information, see https://learn.microsoft.com/en-us/help/platform/learn-editor-add-metadata
# For valid values of ms.service, ms.prod, and ms.topic, see https://learn.microsoft.com/en-us/help/platform/metadata-taxonomies

title:       # Add a title for the browser tab
description: # Add a meaningful description for search results
author:      ridalwan # GitHub alias
ms.author:   rinku.dalwani # Microsoft alias
ms.service:  # Add the ms.service or ms.prod value
# ms.prod:   # To use ms.prod, uncomment it and delete ms.service
ms.topic:    # Add the ms.topic value
ms.date:     07/01/2025
---

# Use RDP Multipath to improve connections to Windows 365 Cloud PC

## Overview

RDP Multipath enhances session reliability and performance in Windows 365 by intelligently managing multiple network paths. This feature ensures users experience smoother, more consistent connections—especially in environments with variable network conditions.

RDP Multipath is built on top of RDP Shortpath and uses Interactive Connectivity Establishment (ICE) to evaluate and select the most reliable transport path in real time.

> [!IMPORTANT]
> __RDP Multipath is now Generally Available (GA).__ We are currently rolling out this connection-level feature to production in a phased manner. Until the rollout reaches 100%, you may not experience RDP Multipath consistently across all connections. The progression to each new phase will be quality-driven, ensuring a stable and reliable experience throughout the deployment.

### Benefits

- __Seamless integration__: No configuration changes are needed beyond ensuring your environment supports RDP Shortpath. For more information, see our blog on [optimizing RDP connectivity](https://techcommunity.microsoft.com/discussions/windows365discussions/optimizing-rdp-connectivity-for-windows-365/3554327)..

- __Intelligent path management__: ICE discovers and evaluates multiple RDP Shortpath routes using STUN (Simple Traversal Underneath NAT) and TURN (Traversal Using Relays around NAT) protocols.

- __Enhanced reliability__: Backup paths remain on standby. If the active path becomes unstable or fails, RDP Multipath automatically switches to the next best path, reducing session drops and interruptions.

> [!IMPORTANT]
> If all paths fail due to a local network outage, the system will attempt to reconnect once connectivity is restored.

### How does this work?

RDP Multipath leverages redundant links based on the paths available, discovered using ICE (Interactive Connectivity Establishment). The active and redundant paths may consist of combinations such as UDP over STUN or UDP over Relay, or multiple UDP over Relay. If the active path breaks, the system will move to the next optimized redundant path. Once all the links are broken, the auto reconnect flow will be initiated. This approach significantly improves connectivity reliability and. However, in situations where all network paths are broken, such as a host router failure or network flap within the user's network setup, users will experience a disconnect and will be auto reconnected once network paths are available. Users relying solely on WebSocket (TCP based) connections will also not benefit from this version of Multipath. Support for TCP based connectivity scenarios will be available in future updates.  
  
![Multipath diagram](media/rdp-multipath/multipath-diagram.png)

In this user scenario, the primary active path is the connection of UDP via STUN, supplemented by two redundant UDP connections through a TURN server.

### Requirements

- __Enable RDP Shortpath for public networks:__ To enable RDP Shortpath for public networks, visit the following page and follow the instructions - [Enable RDP Shortpath for public networks](/azure/virtual-desktop/rdp-shortpath?tabs=public-networks).

- __Client Version__: Requires the latest version of the Remote Desktop client (MSRDC) or Windows App, starting from the January 2025 release (version 1.2.6074 or later)..

### Verify RDP Multipath is used

Users can check the connection status of a remote session from the connection bar, which shows RDP Multipath is enabled, as shown in the following example screenshot:

![A screenshot of connection information showing that RDP Multipath is enabled.](https://review.learn.microsoft.com/en-us/azure/virtual-desktop/media/rdp-multipath/rdp-multipath-connection-bar.png)

### Opt-in or Opt-out of the RDP Multipath

RDP Multipath is being rolled out in phases. If you’d like to manually control the feature availability on your session hosts, you can use the following registry key to either opt in or opt out.

#### Opt-in to RDP Multipath

To enable RDP Multipath ahead of the full rollout, set the following registry key value to 100:

```
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\RdpCloudStackSettings" /v SmilesV3ActivationThreshold /t REG_DWORD /d 100 /f
```

#### Opt-out of RDP Multipath

To enable RDP Multipath ahead of the full rollout, set the following registry key value to 100:  

```
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\RdpCloudStackSettings" /v SmilesV3ActivationThreshold /t REG_DWORD /d 0 /f
```

  
### 

> [!NOTE]
> After updating the registry key, users must disconnect and reconnect to the session host for the change to take effect.

### 

