---
title: 连接到 DB2 (DB2ToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9d485fd0-ab5d-402a-a59a-e9982a61b7de
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5d6ba7b6cb1440a918160dbd9660930d4896a8d7
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-db2-db2tosql"></a>连接到 DB2 (DB2ToSQL)
使用**连接到 DB2**对话框中，连接到你想要迁移的 DB2 数据库。  
  
若要访问此对话框中，在**文件**菜单上，选择**连接到 DB2**。 如果你以前连接，则命令是**重新连接到 DB2**。  
  
## <a name="options"></a>选项  
**提供程序**  
选择你连接到 DB2 数据库的数据访问提供程序。 可用的提供程序是 DB2 客户端提供程序和 OLE DB 访问接口。 默认值为 DB2 客户端提供程序。  
  
**模式**  
选择标准、 TNSNAME 或连接字符串的模式。  
  
-   在标准模式下，你可以输入或选择提供程序、 服务器名称、 服务器端口、 DB2 SID、 用户名称和密码值。  
  
-   在 TNSNAME 模式下，你输入 DB2 数据库、 用户名和密码的连接的标识符 （TNS 别名）。  
  
-   在连接字符串模式下，你提供连接字符串。  
  
    > [!IMPORTANT]  
    > 不建议你使用连接字符串模式，因为文本可能包括密码，并且它以明文形式发送。  
  
默认值为标准模式。  
  
**服务器名称**  
输入的 DB2 服务器名称。 默认服务器名称为与计算机名称相同。 这是标准模式选项。  
  
**服务器端口**  
如果将 1521 （默认值） 以外的端口号用于连接到 DB2，输入端口号。 这是标准模式选项。  
  
**连接标识符**  
输入 DB2 连接标识符。 这是数据库的别名，因为在本地 tnsnames.ora 文件中定义。  
  
这是 TNSNAME 模式选项。  
  
**DB2 SID**  
输入数据库的 SID。 SID 是区别开来的计算机上的 DB2 数据库的标识符。 数据库的默认值 SID 是数据库名称的前八个字符。  
  
这是标准模式选项。  
  
**用户名**  
输入 SSMA 将用于连接到 DB2 数据库的用户名称。  
  
**密码**  
输入用户名的密码。  
  
**连接字符串**  
> [!IMPORTANT]  
> 不建议你使用连接字符串模式，因为文本可能包括密码，并且它以明文形式发送。  
  
如果使用连接字符串模式时，输入完整连接字符串连接到 DB2。  
  
连接字符串由参数名称和值对组成。  
  
-   OLE DB 连接字符串信息，请参阅[Microsoft OLE DB Provider for DB2](http://go.microsoft.com/fwlink/?LinkId=85640) MSDN 库上的文章。  
  
SSMA 连接字符串，始终包含提供程序参数。 此外，请确保连接到 DB2 时包括 Port 参数。  
  
