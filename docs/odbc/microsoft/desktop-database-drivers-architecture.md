---
title: "桌面数据库驱动程序体系结构 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e4da82298313f27adc74f8712895b1777db5078f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="desktop-database-drivers-architecture"></a>桌面数据库驱动程序体系结构
这些驱动程序旨在为使用在 Microsoft Windows 95 或更高版本，或 Windows NT 4.0 和 Windows 2000。 唯一的 32 位应用程序支持 Windows 95 或更高版本;在 Windows NT 4.0 和 Windows 2000 上支持 16 位和 32 位应用程序。  
  
> [!NOTE]  
>  有关 ODBC 用于这些驱动程序的版本有关的信息，请参阅*ODBC 程序员参考*，和过去和当前的发行说明。 除了设定区域，这些驱动程序符合*ODBC 程序员参考*。  
  
 ODBC 桌面数据库驱动程序包括用于 Microsoft Access、 dBASE、 Microsoft Excel、 Paradox 和文本的 32 位驱动程序。 附带的否 16-位驱动程序。 （用于 Microsoft FoxPro 的驱动程序时可用单独。）  
  
 Windows 95 或更高版本的应用程序/驱动程序体系结构是：  
  
 ![应用程序 &#47; 驱动程序体系结构： Windows 95 和更高版本](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 不支持的 Windows 95 上的 16 位应用程序通过这些驱动程序使用。  
  
 在 Windows NT 4.0 和 Windows 2000 上的应用程序/驱动程序体系结构是：  
  
 ![应用程序 &#47; 驱动程序体系结构： NT 4.0 和 Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 桌面数据库驱动程序是两层驱动程序。 在两层配置中，该驱动程序不执行分析、 验证、 优化和执行查询的过程。 相反，Microsoft Jet 执行这些任务。 它处理 ODBC API 调用，并且可作为 SQL 引擎。 Microsoft Jet 已变得驱动程序的整型、 不可分割组成部分： 它随驱动程序，并且位于的驱动程序，即使计算机上的任何其他应用程序使用它。  
  
 桌面数据库驱动程序由六个不同的驱动程序 — 或更确切地说，一个驱动程序文件 (Odbcjt32.dll)，ODBC[驱动程序管理器](../../odbc/reference/the-driver-manager.md)使用六个不同的方式。 数据源的注册表项中的 DRIVERID 标志确定哪些驱动程序中 Odbcjt32.dll 驱动程序管理器使用。 应用程序将对的调用中包含的连接字符串中传递此标志**SQLDriverConnect**。 默认情况下，该标志是 Microsoft Access 驱动程序的 ID。  
  
 驱动程序安装程序文件在安装时更改 DRIVERID 标志。 除 Microsoft Access 驱动程序以外的所有驱动程序具有关联的安装程序 DLL。 当你单击**安装**中[Microsoft ODBC 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)对于数据源，ODBC 安装程序 DLL (Odbcinst.dll) 加载安装程序 DLL。 安装程序 DLL 导出 ODBC 安装程序函数**SQLConfigDataSource**。 如果窗口句柄传递给**SQLConfigDataSource**，此函数显示安装程序窗口，并更改 DRIVERID 标志，根据从用户界面选定的驱动程序。  
  
 如果以编程方式创建了文件，将 NULL 窗口句柄传递给**SQLConfigDataSource**，该函数将创建数据源动态地更改根据 DRIVERID 标志和*lpszDriver*函数调用中的自变量。  
  
 Odbcjt32.dll 实现 ODBC 函数基于 Microsoft Jet API。 没有直接映射之间 ODBC 和 Microsoft Jet 函数，但是所示。 许多因素，如的游标模型和 SQL 映射，防止直接关联的函数。  
  
 Microsoft Jet 引擎和 ODBC 驱动程序管理器之间驻留的 ODBC 驱动程序。 为应用程序调用某些 ODBC 函数处理由驱动程序管理器中且不会传递给该驱动程序。 有关这些函数中，Microsoft Jet 永远看不见函数调用，因为它没有直接连接到的驱动程序管理器。
