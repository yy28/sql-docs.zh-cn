---
description: 桌面数据库驱动程序体系结构
title: 桌面数据库驱动程序体系结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d330392424b683e24f17bd959d0a29e76eedbd36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449569"
---
# <a name="desktop-database-drivers-architecture"></a>桌面数据库驱动程序体系结构
这些驱动程序设计用于 Microsoft Windows 95 或更高版本，或者 Windows NT 4.0 和 Windows 2000。 Windows 95 或更高版本仅支持32位应用程序;Windows NT 4.0 和 Windows 2000 上支持16位和32位应用程序。  
  
> [!NOTE]  
>  有关这些驱动程序要使用的 ODBC 版本的信息，请参阅 *Odbc 程序员参考*，以及以前和当前的发行说明。 除了注释区域，这些驱动程序都符合 *ODBC 程序员的参考*。  
  
 ODBC 桌面数据库驱动程序包括 Microsoft Access、dBASE、Microsoft Excel、Paradox 和文本的32位驱动程序。 不包含16位驱动程序。  (Microsoft FoxPro 的驱动程序单独提供。 )   
  
 Windows 95 或更高版本上的应用程序/驱动程序体系结构为：  
  
 ![应用&#47;驱动程序体系结构： Windows 95 及更高版本](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 不支持通过 Windows 95 上的16位应用程序使用这些驱动程序。  
  
 Windows NT 4.0 和 Windows 2000 上的应用程序/驱动程序体系结构为：  
  
 ![应用&#47;驱动程序体系结构： NT 4.0 和 Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 桌面数据库驱动程序是双层驱动程序。 在两层配置中，驱动程序不执行分析、验证、优化和执行查询的过程。 相反，Microsoft Jet 会执行这些任务。 它处理 ODBC API 调用并充当 SQL 引擎。 Microsoft Jet 已成为驱动程序的一个有机组成部分，不可分割是驱动程序附带的驱动程序，即使计算机上没有其他应用程序使用它也是如此。  
  
 桌面数据库驱动程序包含六个不同的驱动程序，或者更准确地说，ODBC [驱动程序管理器](../../odbc/reference/the-driver-manager.md) 使用六种不同的方法 ( # A0) 。 数据源的注册表项中的 DRIVERID 标志确定驱动程序管理器 Odbcjt32.dll 使用哪一个驱动程序。 应用程序将此标志传递到对 **SQLDriverConnect**的调用中包含的连接字符串中。 默认情况下，该标志是 Microsoft Access 驱动程序的 ID。  
  
 驱动程序安装程序文件在安装时更改 DRIVERID 标志。 除 Microsoft Access 驱动程序之外的所有驱动程序都具有关联的安装 DLL。 在数据源的[MICROSOFT ODBC 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)中单击 "**安装**" 时，ODBC 安装程序 dll ( # A0) 加载安装程序 dll。 安装程序 DLL 导出 ODBC 安装程序函数 **SQLConfigDataSource**。 如果将窗口句柄传递到 **SQLConfigDataSource**，则此函数将显示安装窗口，并根据从用户界面中选择的驱动程序更改 DRIVERID 标志。  
  
 以编程方式创建文件时，空窗口句柄会传递到 **SQLConfigDataSource**，而函数会动态创建数据源，并根据函数调用中的 *LPSZDRIVER* 参数更改 DRIVERID 标志。  
  
 Odbcjt32.dll 在 Microsoft Jet API 之上实现 ODBC 函数。 不过，ODBC 和 Microsoft Jet 函数之间没有直接映射。 许多因素（如游标模型和 SQL 映射）会阻止函数的直接关联。  
  
 ODBC 驱动程序驻留在 Microsoft Jet 引擎和 ODBC 驱动程序管理器之间。 应用程序调用的某些 ODBC 函数由驱动程序管理器处理，不会传递给驱动程序。 对于这些函数，Microsoft Jet 永远无法看到函数调用，因为它没有与驱动程序管理器的直接连接。
