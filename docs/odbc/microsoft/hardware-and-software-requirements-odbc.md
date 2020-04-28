---
title: 硬件和软件要求（ODBC） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81295237"
---
# <a name="hardware-and-software-requirements-odbc"></a>硬件和软件要求 (ODBC)
本主题列出了使用 ODBC 桌面数据库驱动程序的要求。  
  
## <a name="hardware-requirements"></a>硬件要求  
 若要使用 ODBC 桌面数据库驱动程序，您必须：  
  
-   与 IBM 兼容的个人计算机。  
  
-   硬盘有 6 MB 的可用磁盘空间。  
  
-   至少 16 MB 的随机存取内存（RAM）。  
  
## <a name="software-requirements"></a>软件要求  
 若要使用 ODBC 驱动程序访问数据，您必须具有：  
  
-   ODBC 驱动程序。  
  
-   32位 ODBC 驱动程序管理器版本3.51 或更高版本（Odbc32.lib）。  
  
-   Microsoft Windows 95 或更高版本，或者 Windows NT 4.0 或 Windows 2000。  
  
-   使用 Microsoft ODBC 驱动程序的应用程序的堆栈大小至少为 20 KB。  
  
 使用 Microsoft Windows NT 4.0 或 Windows 2000 时，32位驱动程序是线程安全的，但仅通过使用控制对驱动程序的访问的全局信号量来完成。 在 Windows NT 下，对驱动程序的并发使用非常有限。 对于使用 Microsoft Jet 引擎的所有应用程序，对 Jet ISAM 层的所有访问都是单线程的。  
  
 在 Microsoft Windows NT 4.0 上的 windows on windows （WOW）上运行多个16位应用程序时，应用程序必须在单独的内存空间中运行。 （由于 ODBC 不支持同一进程中的多个环境，因此不能使用相同的内存空间。）若要在单独的内存空间中运行应用程序，请在程序管理器中选择该应用程序的图标，打开 "**文件**" 菜单，然后单击 "**属性**"，然后单击 "**在单独的内存空间中运行**"。  
  
 不支持通过 Windows 95 上的16位应用程序使用这些驱动程序。  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>特定于驱动程序的硬件和软件要求  
  
-   MicrosoftAccess 和 dBASEdrivers 可能需要在 Autoexec.bat 或 config.sys 文件中进行更改。
