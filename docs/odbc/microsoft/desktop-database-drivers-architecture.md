---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7487d073b95190418ee7f6900390a2d60ce42e13
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516858"
---
# <a name="desktop-database-drivers-architecture"></a>桌面数据库驱动程序体系结构
这些驱动程序旨在用于使用 Microsoft Windows 95 或更高版本，或 Windows NT 4.0 和 Windows 2000。 仅 32 位应用程序支持 Windows 95 上或更高版本;在 Windows NT 4.0 和 Windows 2000 上支持 16 位和 32 位应用程序。  
  
> [!NOTE]  
>  有关与这些驱动程序一起使用的 ODBC 版本信息，请参阅*ODBC 程序员参考*，和以前和当前的发行说明。 这些驱动程序符合所述的区域除外*ODBC 程序员参考*。  
  
 ODBC 桌面数据库驱动程序的 Microsoft Access、 dBASE、 Microsoft Excel、 Paradox，文本包括 32 位驱动程序。 包含任何 16 位驱动程序。 （Microsoft FoxPro 的驱动程序是可单独。）  
  
 Windows 95 上或更高版本的应用程序/驱动程序体系结构是：  
  
 ![应用&#47;驱动程序体系结构：Windows 95 和更高版本](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 不支持使用这些驱动程序通过 Windows 95 上的 16 位应用程序。  
  
 在 Windows NT 4.0 和 Windows 2000 上的应用程序/驱动程序体系结构是：  
  
 ![应用&#47;驱动程序体系结构：NT 4.0 和 Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 桌面数据库驱动程序是双层驱动程序。 在两层配置中，该驱动程序不执行分析、 验证、 优化和执行查询的过程。 相反，Microsoft Jet 执行这些任务。 它处理 ODBC API 调用，并充当 SQL 引擎。 Microsoft Jet 已成为整数且不可分割的驱动程序的一部分：它随驱动程序，并驻留的驱动程序，即使在计算机上的没有其他应用程序使用它。  
  
 桌面数据库驱动程序包含六个不同的驱动程序-或者，更确切地说，一个驱动程序文件 (Odbcjt32.dll) 的 ODBC[驱动程序管理器](../../odbc/reference/the-driver-manager.md)使用六个不同的方式。 数据源的注册表项中的 DRIVERID 标志确定 Odbcjt32.dll 中的哪些驱动程序的驱动程序管理器使用。 应用程序将此标志传递到调用中包含的连接字符串中**SQLDriverConnect**。 默认情况下，该标志是 Microsoft Access 驱动程序的 ID。  
  
 驱动程序安装程序文件在安装时更改 DRIVERID 标志。 除 Microsoft Access 驱动程序以外的所有驱动程序必须无关联的安装程序 DLL。 当您单击**安装程序**中[Microsoft ODBC 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)对于数据源、 ODBC 安装程序 DLL （系统） 加载安装程序 DLL。 安装程序 DLL 导出 ODBC 安装程序函数**SQLConfigDataSource**。 如果窗口句柄传递给**SQLConfigDataSource**，此函数将显示安装程序窗口，并更改 DRIVERID 标志根据从用户界面选定的驱动程序。  
  
 以编程方式创建文件时，NULL 窗口句柄传递给**SQLConfigDataSource**，并且该函数将创建数据源动态地更改根据 DRIVERID 标志*lpszDriver*函数调用中的参数。  
  
 Odbcjt32.dll 实现基于 Microsoft Jet API 的 ODBC 函数。 存在但是是 ODBC 和 Microsoft Jet 函数之间没有直接的映射。 许多因素，例如游标模型和 SQL 映射，防止直接相关的函数。  
  
 ODBC 驱动程序驻留在 Microsoft Jet 引擎和 ODBC 驱动程序管理器之间。 通过应用程序调用某些 ODBC 函数处理由驱动程序管理器中，不会传递给驱动程序。 有关这些函数中，Microsoft Jet 永远看不见函数调用，因为它没有直接连接到驱动程序管理器。
