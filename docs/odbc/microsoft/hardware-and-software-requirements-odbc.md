---
title: 硬件和软件要求 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- hardware requirements [ODBC], desktop database drivers
- software requirements [ODBC], desktop database drivers
- system requirements [ODBC], desktop database drivers
- requirements [ODBC], desktop database drivers
ms.assetid: 6df2e9cd-de10-4629-97bd-32f2782616c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3f40621645aad2d1e52cb0a89baa8ff29b01446
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680655"
---
# <a name="hardware-and-software-requirements-odbc"></a>硬件和软件要求 (ODBC)
本主题列出了使用 ODBC 桌面数据库驱动程序的要求。  
  
## <a name="hardware-requirements"></a>硬件要求  
 若要使用 ODBC 桌面数据库驱动程序，必须具有：  
  
-   将 IBM 兼容的个人计算机。  
  
-   包含 6 MB 的可用磁盘空间的硬盘。  
  
-   至少 16 MB 的随机存取内存 (RAM)。  
  
## <a name="software-requirements"></a>软件要求  
 若要访问使用 ODBC 驱动程序的数据，必须具有：  
  
-   ODBC 驱动程序。  
  
-   32 位 ODBC 驱动程序管理器，版本 3.51 或更高版本 (所用的 Odbc32.dll)。  
  
-   Microsoft Windows 95 或更高版本，或 Windows NT 4.0 或 Windows 2000。  
  
-   至少 20 KB 使用 Microsoft ODBC 驱动程序的应用程序的堆栈大小。  
  
 在使用 Microsoft Windows NT 4.0 或 Windows 2000，32 位驱动程序是线程安全的但只能通过使用全局信号量，控制对该驱动程序的访问。 功能非常有限的驱动程序同时使用 Windows NT 下。 对 Jet ISAM 层的所有访问将都是单线程的所有应用程序使用 Microsoft Jet 引擎。  
  
 在 Windows on Windows (WOW) 在 Microsoft Windows NT 4.0 上运行多个 16 位应用程序，必须在独立的内存空间中运行应用程序。 （由于 ODBC 不支持在同一进程中的多个环境，不能使用相同的内存空间。）若要在单独的内存空间中运行应用程序，选择应用程序的图标中的程序管理器，打开**文件**菜单，然后单击**属性**，然后单击**运行在单独的内存空间**。  
  
 不支持使用这些驱动程序通过 Windows 95 上的 16 位应用程序。  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>特定于驱动程序硬件和软件要求  
  
-   MicrosoftAccess 和 dBASEdrivers 可能需要的 Autoexec.bat 或 Config.sys 文件中的更改。
