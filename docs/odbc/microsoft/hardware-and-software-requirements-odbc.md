---
title: "硬件和软件要求 (ODBC) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hardware requirements [ODBC], desktop database drivers
- software requirements [ODBC], desktop database drivers
- system requirements [ODBC], desktop database drivers
- requirements [ODBC], desktop database drivers
ms.assetid: 6df2e9cd-de10-4629-97bd-32f2782616c7
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7cee0668d49ba0edb88d21799ec571aa708259dd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="hardware-and-software-requirements-odbc"></a>硬件和软件要求 (ODBC)
本主题列出使用 ODBC 桌面数据库驱动程序的要求。  
  
## <a name="hardware-requirements"></a>硬件要求  
 若要使用 ODBC 桌面数据库驱动程序，你必须具有：  
  
-   无 IBM 兼容的个人计算机。  
  
-   具有 6 MB 的可用磁盘空间的硬盘。  
  
-   至少 16 MB 的随机存取存储器 (RAM)。  
  
## <a name="software-requirements"></a>软件要求  
 若要访问带有 ODBC 驱动程序的数据，你必须具有：  
  
-   ODBC 驱动程序。  
  
-   32 位 ODBC 驱动程序管理器，3.51 版或更高版本 (所用的 Odbc32.dll)。  
  
-   Microsoft Windows 95 或更高版本、 或 Windows NT 4.0 或 Windows 2000。  
  
-   至少 20 KB 使用 Microsoft ODBC 驱动程序的应用程序的堆栈大小。  
  
 在使用 Microsoft Windows NT 4.0 或 Windows 2000，32 位驱动程序是线程安全的但仅通过全局信号量控制访问驱动程序使用。 驱动程序的并发使用是非常有限 Windows NT 下。 到 Jet ISAM 层的所有访问权限将单线程方式对于使用 Microsoft Jet 引擎的所有应用程序。  
  
 当在 Windows 上 Windows (WOW) 在 Microsoft Windows NT 4.0 上运行多个 16 位应用程序，必须在单独的内存空间运行应用程序。 （因为 ODBC 不支持在相同的进程中使用多个环境，不能使用相同的内存空间。）若要在单独的内存空间中运行应用程序，选择应用程序的图标中的程序管理器，打开**文件**菜单，然后单击**属性**，然后单击**运行在单独的内存空间**。  
  
 不支持的 Windows 95 上的 16 位应用程序通过这些驱动程序使用。  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>特定于驱动程序的硬件和软件要求  
  
-   MicrosoftAccess 和 dBASEdrivers 可能需要 Autoexec.bat 或 Config.sys 文件中的更改。
