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

# Use RDP Multipath to Improve Windows 365 Cloud PC Connections

RDP Multipath is now generally available for Windows 365, bringing enhanced network resiliency and seamless connectivity to Cloud PCs. This feature is being rolled out in phases across Windows 365 tenants.

RDP Multipath dynamically evaluates multiple UDP network paths and intelligently switches to the most reliable one—before a connection drop occurs. This ensures a smoother and more stable user experience, especially in environments with fluctuating network conditions.

### Requirements

- **Enable RDP Shortpath for public networks:**  To enable RDP Shortpath for public networks, visit the following Azure Virtual Desktop documentation page and follow the instructions - [Enable RDP Shortpath for public networks](/azure/virtual-desktop/rdp-shortpath?tabs=public-networks).

- **Client Version**: Requires the latest version of the Remote Desktop client (MSRDC) or Windows App, starting from the January 2025 release (version 1.2.6074 or later).

### Key Benefits

- **Seamless Integration**: No configuration changes are required. RDP Multipath is enabled by default for supported clients.

- **Intelligent Path Management**: Continuously monitors multiple UDP paths and proactively selects the best-performing one.

- **Improved Reliability**: Reduces the risk of session drops and improves connection stability for Cloud PC users.

### Deployment Phases

RDP Multipath for Windows 365 is being introduced through a **phased, production-based rollout**. This quality-led approach ensures a stable and reliable experience across environments by allowing Microsoft to monitor performance and address any issues before broader deployment.

- **Phased General Availability**: RDP Multipath is progressively enabled across Windows 365 tenants. No action is required from IT administrators during this phase.

- **Full Availability**: Once telemetry confirms performance and stability benchmarks are met, RDP Multipath becomes enabled for all supported Windows 365 environments.

This approach ensures that the feature delivers improved session resiliency and seamless connectivity before it becomes universally available.

### Verify RDP Multipath is used

There are two ways to verify that RDP Multipath is being used for a connection:

Users can check the connection status of a remote session from the connection bar, which shows RDP Multipath is enabled, as shown in the following example screenshot:

![A screenshot of connection information showing that RDP Multipath is enabled.](https://review.learn.microsoft.com/en-us/azure/virtual-desktop/media/rdp-multipath/rdp-multipath-connection-bar.png)

### Opt-out of the RDP Multipath

If you prefer to disable the RDP Multipath feature until it is fully rolled out, you can opt out at the session host level using the following registry key.


```
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\RdpCloudStackSettings" /v SmilesV3ActivationThreshold /t REG_DWORD /d 0 /f
```

### Next steps

For complete information, see [Azure Virtual Desktop RDP Multipath](/windows-365/enterprise/rdp-shortpath-public-networks) 

