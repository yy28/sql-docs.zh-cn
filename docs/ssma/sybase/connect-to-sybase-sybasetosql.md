---
title: 连接到 Sybase (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0630bf5c7987c65eab321da888f297e8d72b734b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-sybase-sybasetosql"></a>连接到 Sybase (SybaseToSQL)
使用**连接到 Sybase**对话框中，若要连接到你想要迁移的 Sybase 自适应 Server Enterprise (ASE) 实例。  
  
若要访问此对话框中，在**文件**菜单上，选择**连接到 Sybase**。 如果你以前连接，则命令是**重新连接到 Sybase**。  
  
## <a name="options"></a>选项  
**提供程序**  
选择任何用于连接到 Sybase 服务器计算机上安装提供程序。  
  
**模式**  
选择任何一种标准或高级连接模式。 在标准模式下，你可以输入或选择服务器名称、 端口、 用户名称和密码值。 在高级模式中，你提供的连接字符串。  
  
**服务器名称**  
输入或选择的名称或自适应服务器 IP 地址。 默认服务器名称为与计算机名称相同。 这是标准模式选项。  
  
**服务器端口**  
如果将非默认端口用于连接到 ASE，输入端口号。 默认端口号为 5000。 这是标准模式选项。  
  
**用户名**  
输入用于连接到 ASE 的用户名称。 这是标准模式选项。  
  
**密码**  
输入用户名的密码。 这是标准模式选项。  
  
**连接字符串**  
输入连接到 ASE 完整连接字符串。  
  
连接字符串由参数名称和值对组成。 参数的名称因所使用的提供程序而异。  
  
**各种供应商的连接参数如下所示：**  
  
1.  连接参数**OLE DB 提供程序**  
  
    |设置|Sybase 12.5 参数|Sybase 15 参数|  
    |-----------|-------------------------|-----------------------|  
    |服务器名称|服务器名称|Server|  
    |端口|服务器端口地址|端口|  
    |用户名|用户 ID|用户 ID|  
    |密码|密码|密码|  
    |提供程序|提供程序|提供程序|  
  
    Sybase ASE 12.5 的一个示例连接字符串如下所示：  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    Sybase ASE 15 个，如下所示是一个示例连接字符串：  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  连接参数**ODBC 提供程序**  
  
    |设置|Sybase 12.5 月 15 日参数|  
    |-----------|-----------------------------|  
    |驱动程序名称|驱动程序|  
    |服务器名称|Server|  
    |用户名|uid|  
    |密码|pwd|  
    |端口号|端口|  
  
    对于 Sybase ASE 12.5 或 15 中，连接字符串的示例如下所示：  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  连接参数**ADO.NET 提供程序**  
  
    |设置|Sybase 12.5 月 15 日参数|  
    |-----------|-----------------------------|  
    |服务器名称|Server|  
    |用户名|uid|  
    |密码|pwd|  
    |端口号|端口|  
  
    请按照是的 ADO.NET 提供程序的连接字符串示例：  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
有关详细信息，请参阅 ASE 文档。  
  
这是一个高级的模式选项。  
  
