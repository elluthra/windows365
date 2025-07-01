---
# required metadata
title: Connection endpoints for Windows 365 Link
titleSuffix:
description: Learn about connection endpoints for Windows 365 Link
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/01/2025
ms.topic: overview
ms.service: windows-365-link
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: sajelaci
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started; intro-hub-or-landing
ms.collection:
- M365-identity-device-management
- tier2
---

# Connection endpoints for Windows 365 Link

Some Windows 365 Link components, apps, and related services transfer data to Microsoft network endpoints. This article lists different endpoints and URLs that must be allowed in your network configuration (proxy or firewall) for those components to function.

These endpoints are required to be accessed by the Windows 365 Link device. If a proxy server is used in between the Link device and the internet, these endpoints must have authentication bypassed. The Windows 365 Link device won't support proxy authentication because many of these endpoints are needed without a user context (like during the logon process or before a user authenticates).

This list is designed as a starting point for your network connectivity. Windows 365, Intune, and Microsoft Entra ID are evolving services and changes can occur regularly. Check the service pages linked to from this page frequently in case updates are made. Your own configurations might require adding more URLs. When troubleshooting make sure that your network engineers:

- Can validate connections made from the Link device.
- Identify if other URLs or connectivity must be allowed.  

The following methodology was used to derive these network endpoints:  

1. Unbox and plug in Windows 365 Link with an ethernet cable.
2. Begin a Windows Update cycle to ensure the latest version of the OS (tested in May 2025).
3. Join a representative Microsoft Entra and Intune tenant, and connect to a Windows 365 Cloud PC.
4. Use the device at various times for one week, including various Intune commands (like Reset, Collect Diagnostics, Sync, and so on).
5. All HTTP/(S) requests were captured at the internet egress.
6. Other endpoints are added from the relevant Intune / Windows documentation to support global regions.

| Purpose | Endpoints required |
| --- | --- |
|  Authentication. These endpoints must authenticate with Microsoft Entra ID to perform Microsoft Entra join and enable user authentication. | login.microsoftonline.com<br>login.live.com<br>www.microsoft.com<br>\*.microsoftaik.azure.net<br>aadcdn.msauth.net<br>aadcdn.msauthimages.net<br>login.microsoft.com<br>aadcdn.msftauth.net<br>graph.windows.net<br> |
|  Connectivity. Network Connection Status Indicator (NCSI) detects internet connectivity and corporate network connectivity status. NCSI sends a DNS request and HTTP query to this endpoint to determine if the device can communicate with the Internet. If you turn off traffic for this endpoint, NCSI can't determine if the device is connected to the internet, and the network status tray icon shows a warning. | www.msftconnecttest.com<br>ipv6.msftconnecttest.com<br> |
|  Security. These endpoints are used for certificate updates, and Microsoft Defender Protections. | ocsp.digicert.com<br>\*.endpoint.security.microsoft.com<br>ctldl.windowsupdate.com<br>mscrl.microsoft.com<br>wdcp.microsoft.com<br>fpt.dfp.microsoft.com<br> |
|  Windows Update  | \*.windowsupdate.com<br>\*.mp.microsoft.com<br>\*.update.microsoft.com<br> |
|  Windows Push Notification Services. WNS enables third-party developers to send toast, tile, badge, and raw updates from their own cloud service. This service provides a mechanism to deliver new updates to your users in a power-efficient and dependable way. If you turn off traffic for this endpoint, push notifications don't work, including MDM device management, mail synchronization, settings synchronization. | \*.wns.windows.com<br>\*.notify.windows.com<br> |
|  Location. The following endpoint is used for location data. If you turn off traffic for this endpoint, Windows 365 Link can't detect its current location (or time zone) | inference.location.live.net<br> |
|  [Intune](/intune/intune-service/fundamentals/intune-endpoints)  | Manage.microsoft.com<br>\*.manage.microsoft.com<br>\*.mp.microsoft.com<br>Ecs.office.com<br>\*.spserv.microsoft.com<br>enterpriseregistration.windows.net<br>certauth.enterpriseregistration.windows.net<br>lgmsapeweu.blob.core.windows.net<br>lgmsapewus2.blob.core.windows.net<br>lgmsapesea.blob.core.windows.net<br>lgmsapeaus.blob.core.windows.net<br>lgmsapeind.blob.core.windows.net<br>\*.attest.azure.net<br>checkin.dm.microsoft.com<br>\*.azureedge.net<br> |
|  [Diagnostic data](windows-cpc-os-privacy-data.md#windows-cpc-diagnostic-data)  | \*.data.microsoft.com<br> |
|  Browser. These endpoints are used by the WebView components within the Link Device. | edge.microsoft.com<br>static.edge.microsoftapp.net<br>edge-cloud-resource-static.azureedge.net<br>edge-mobile-static.azureedge.net<br> |

## Additional service endpoints

### Windows 365

Windows 365 Link connects to the Windows 365 Service. Therefore, the device must connect to the endpoints listed under [End user devices](/azure/virtual-desktop/required-fqdn-endpoint?tabs=azure#end-user-devices).

### Microsoft Teams

The Windows 365 Link device optimizes traffic to Microsoft Teams by offloading media connections directly from the device to the Microsoft Teams service. Therefore, connections must be allowed to the Microsoft Teams services as described in [Microsoft 365 URLs and IP address ranges under Microsoft Teams](/microsoft-365/enterprise/urls-and-ip-address-ranges?view=o365-worldwide#microsoft-teams).

## Additional endpoints

Depending on your configurations, you might need to enable other endpoints not listed here. This could be for many reasons, but may include:

- MMR Call Redirection to third party call center providers.
- Additional authentication services (like ADFS, third party IdPs, or MFA providers).

## Additional ports and network requirements

The Windows 365 Link device might need:

- UDP 53 – DNS
- UDP 67 – DHCP
- UDP 123 – SNTP (Connection to Time.Windows.Com)

<!-- ########################## -->
## Next steps

[Manage Windows 365 Link devices](device-management-overview.md)
