---
title: Computer Management shows clients sessions slow
description: Provides a solution to an issue where information on shared folder sessions is populated slow in Computer Management console.
ms.date: 09/17/2020
author: Deland-Han
ms.author: delhan
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: kaushika, DanMa
ms.prod-support-area-path: Access to remote file shares (SMB or DFS Namespace)
ms.technology: Networking
---
# You may have to wait for a long time to populate the information on shared folder sessions in Computer Management console

This article provides a solution to an issue where information on shared folder sessions is populated slow in Computer Management console.

_Original product version:_ &nbsp; Windows Server 2012 R2  
_Original KB number:_ &nbsp; 2454039

## Symptoms

When trying to view the information about client sessions by clicking Shared Folders -> Sessions in the Computer Management console, it may take a long time to populate the information, and the console may stop responding or appear to hang.

## Cause

Computer Management will try to resolve the client IP address to user-friendly NetBIOS name. In and IPv6 and IPv4 hybrid environment, and clients use [\\\NetBIOS](file://netbios/)  to access share folders, if the NetBIOS name cannot be resolved, it shows the IPv6 address immediately. However, if clients are using [\\\IPv4](file://ipv4/) to access share folder, the failure of resolving to the NetBIOS name causes the Computer Management console to hang.

## Resolution

1. Disable NetBIOS over TCP/IP:

    1. Run ncpa.cpl
    2. Right-click the NIC 
    3. select properties
    4. click TCPIPV4
    5. click advanced
    6. click WINS
    7. choose Disable Netbios over TCPIP

2. Configure reverse lookup zone in DNS server. It is useful to computers that are added in domain.