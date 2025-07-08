---
# required metadata
title: Certificates and networking for Windows 365 Link devices
titleSuffix:
description: Learn about certificates and networking for Windows 365 Link devices
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 06/26/2025
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

# Certificates and networking

Organizations can use Intune to assign certificates and configure Network settings on Windows 365 Link devices. These policies can be the same Intune policies that have already been used with Windows 11 devices that are Microsoft Entra joined.

If your current implementation relies on AD joined devices and group policy, first test the deployment of your Wi-Fi or Ethernet settings to a Microsoft Entra joined and Intune-managed Windows 11 device. If such testing reveals issues, it's simpler to troubleshoot on Windows 11 than a Windows 365 Link device.

## Certificates

Windows 365 Link supports the same certificate policies for authentication as Windows 11. Intune can be used for:

- Trusted certificate installation.
- Public Key Cryptography Standards (PKCS) certificates.
-Simple Certificate Enrollment Protocol (SCEP) certificates.

Most certificate policies that work with Microsoft Entra joined Windows 11 devices also work on Windows 365 Link.

Windows 365 Link is a shared device. Therefore, you should deploy device certificates instead of user certificates for Wi-Fi Authentication.

For more information, see [Types of certificate that are supported by Microsoft Intune](/intune/intune-service/protect/certificates-configure).

## Networking

Windows 365 Link supports the same policies for Wi-Fi and wired networks as Windows 11. This support includes the Basic profile and Enterprise profiles that use certificates for authentication. Most Wi-Fi policies that work with Microsoft Entra joined Windows 11 devices also work on Windows 365 Link.

For more information, see [Wi-Fi settings for Windows 10/11 devices in Microsoft Intune](/intune/intune-service/configuration/wi-fi-settings-windows) and [Configure wired network settings for Windows devices in Microsoft Intune](/intune/intune-service/configuration/wired-network-settings-windows).

> [!NOTE]
> Windows 365 Link doesn't support the use of username/password for network authentication, like MS-CHAP v2. This method uses the same response function as the deprecated NTLMv1 network authentication. Windows 365 Link doesn't support EAP-MSCHAPv2 or PEAP-MSCHAPv2 for authentication. Instead of using these protocols, we recommend that you use certificate based authentication like EAP-TLS or PEAP-TLS.

## Proxy

Windows 365 Link supports the same policies for Network Proxy as Windows 11, but users can't be prompted for authentication with the proxy. Most proxy policies that work with Microsoft Entra joined Windows 11 devices also work on Windows 365 Link.

In some cases, a [device restriction policy for proxy settings](/intune/intune-service/configuration/device-restrictions-windows-10#network-proxy) might show as **Not Applicable** when assigned to Link devices. If this result happens, a Custom policy can instead be used to set the network proxy configuration service provider (CSP) OMA-URI values.

For more information, see [NetworkProxy CSP](/windows/client-management/mdm/networkproxy-csp).

<!-- ########################## -->
## Next steps

[Deployment overview](deployment-overview.md)

