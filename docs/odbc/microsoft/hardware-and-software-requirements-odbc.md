---
title: 硬件和软件要求 （ODBC） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe69775e379e9a9d661b4ddf81e577b738fcf34d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295237"
---
# <a name="hardware-and-software-requirements-odbc"></a>硬件和软件要求 (ODBC)
本主题列出了使用 ODBC 桌面数据库驱动程序的要求。  
  
## <a name="hardware-requirements"></a>硬件要求  
 要使用 ODBC 桌面数据库驱动程序，您必须具有：  
  
-   与 IBM 兼容的个人电脑。  
  
-   具有 6 MB 可用磁盘空间的硬盘。  
  
-   至少 16 MB 的随机访问内存 （RAM）。  
  
## <a name="software-requirements"></a>软件要求  
 要使用 ODBC 驱动程序访问数据，您必须具有：  
  
-   ODBC 驱动程序。  
  
-   32 位 ODBC 驱动程序管理器，版本 3.51 或更高版本（Odbc32.dll）。  
  
-   微软视窗 95 或更高版本，或 Windows NT 4.0 或 Windows 2000。  
  
-   使用 Microsoft ODBC 驱动程序的应用程序的堆栈大小至少为 20 KB。  
  
 使用 Microsoft Windows NT 4.0 或 Windows 2000 时，32 位驱动程序是线程安全的，但只能通过使用控制对驱动程序访问的全局信号量。 在 Windows NT 下，驱动程序的并发使用非常有限。 对于使用 Microsoft Jet 引擎的所有应用程序，对 Jet ISAM 层的所有访问都将是单线程的。  
  
 在 Microsoft Windows NT 4.0 上的 Windows 上运行多个 16 位应用程序时，这些应用程序必须在单独的内存空间中运行。 （不能使用相同的内存空间，因为 ODBC 不支持同一进程中的多个环境。要在单独的内存空间中运行应用程序，请在程序管理器中选择应用程序的图标，打开 **"文件**"菜单并单击"**属性**"，然后单击"**在单独的内存空间中运行**"。  
  
 不支持在 Windows 95 上使用 16 位应用程序使用这些驱动程序。  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>特定于驱动程序的硬件和软件要求  
  
-   MicrosoftAccess 和 dBASE 驱动程序可能需要更改 Autoexec.bat 或 Config.sys 文件中。
