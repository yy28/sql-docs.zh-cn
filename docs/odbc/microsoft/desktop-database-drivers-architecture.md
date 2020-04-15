---
title: 桌面数据库驱动程序体系结构 |微软文档
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
ms.openlocfilehash: ae6fb72bb3ed0a9bca1571eb572bbfbd20fe9995
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288737"
---
# <a name="desktop-database-drivers-architecture"></a>桌面数据库驱动程序体系结构
这些驱动程序设计用于 Microsoft Windows 95 或更高版本，或 Windows NT 4.0 和 Windows 2000。 Windows 95 或更高版本仅支持 32 位应用程序;Windows NT 4.0 和 Windows 2000 上支持 16 位和 32 位应用程序。  
  
> [!NOTE]  
>  有关要与这些驱动程序一起使用的 ODBC 版本的信息，请参阅*ODBC 程序员的参考*，以及过去和当前发行说明。 除所述区域外，这些驱动程序符合*ODBC 程序员的参考*。  
  
 ODBC 桌面数据库驱动程序包括用于 Microsoft 访问、dBASE、微软 Excel、悖论和文本的 32 位驱动程序。 不包括 16 位驱动程序。 （微软 FoxPro 的驱动程序单独提供。  
  
 Windows 95 或更高版本上的应用程序/驱动程序体系结构是：  
  
 ![应用&#47;驱动程序体系结构：Windows 95 及更高版本](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 不支持在 Windows 95 上使用 16 位应用程序使用这些驱动程序。  
  
 Windows NT 4.0 和 Windows 2000 上的应用程序/驱动程序体系结构是：  
  
 ![应用&#47;驱动程序体系结构：NT 4.0 和 Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 桌面数据库驱动程序是双层驱动程序。 在两层配置中，驱动程序不执行分析、验证、优化和执行查询的过程。 相反，微软喷气式飞机执行这些任务。 它处理 ODBC API 调用并充当 SQL 引擎。 Microsoft Jet 已经成为驱动程序不可分割的一部分：它与驱动程序一起附带，并驻留在驱动程序中，即使计算机上没有其他应用程序使用它。  
  
 桌面数据库驱动程序由六个不同的驱动程序组成 - 或者更确切地说，一个驱动程序文件 （Odbcjt32.dll），ODBC[驱动程序管理器](../../odbc/reference/the-driver-manager.md)以六种不同的方式使用该文件。 数据源的注册表条目中的 DRIVERID 标志确定驱动程序管理器使用的 Odbcjt32.dll 中的哪个驱动程序。 应用程序在**SQLDriverConnect**调用中包含的连接字符串中传递此标志。 默认情况下，该标志是 Microsoft Access 驱动程序的 ID。  
  
 驱动程序设置文件在设置时更改 DRIVERID 标志。 除 Microsoft Access 驱动程序外，所有驱动程序都有关联的设置 DLL。 当您单击[Microsoft ODBC 数据源管理员](../../odbc/admin/odbc-data-source-administrator.md)中的 **"设置**"数据源时，ODBC 安装程序 DLL （Odbcinst.dll） 将加载安装程序 DLL。 设置 DLL 导出 ODBC 安装程序函数**SQLConfigDataSource**。 如果将窗口句柄传递给**SQLConfigDataSource，** 则此功能将显示一个设置窗口，并根据从用户界面中选择的驱动程序更改 DRIVERID 标志。  
  
 以编程方式创建文件时，NULL 窗口句柄将传递给**SQLConfigDataSource**，并且函数会动态创建数据源，根据函数调用中的*lpszDriver*参数更改 DRIVERID 标志。  
  
 Odbcjt32.dll 在 Microsoft Jet API 之上实现了 ODBC 功能。 但是，ODBC 和 Microsoft Jet 函数之间没有直接映射。 许多因素（如游标模型和 SQL 映射）阻止函数的直接关联。  
  
 ODBC 驱动程序位于 Microsoft Jet 引擎和 ODBC 驱动程序管理器之间。 应用程序调用的某些 ODBC 函数由驱动程序管理器处理，不会传递给驱动程序。 对于这些功能，Microsoft Jet 永远不会看到函数调用，因为它没有与驱动程序管理器的直接连接。
