---
title: "连接字符串格式和属性 |Microsoft 文档"
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
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 40b73ac727b682649f12ac6b70a0256681447622
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="connection-string-format-and-attributes"></a>连接字符串格式和属性
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 而不是使用对话框中，某些应用程序可能需要一个连接字符串，指定数据源连接信息。 连接字符串由大量的指定驱动程序如何连接到数据源的属性组成。 属性用于标识特定的驱动程序需要知道来进行适当的数据源连接的信息。 每个驱动程序可能具有一组不同的属性，但连接字符串的格式都始终相同。 连接字符串具有以下格式：  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  适用于 Oracle 的 Microsoft ODBC 驱动程序支持连接字符串的格式的驱动程序，用于在用户的第一个版本`CONNECTSTRING`= 而不是`SERVER=`。  
  
 如果你要连接到的数据源提供程序支持 Windows 身份验证，你应指定`Trusted_Connection=yes`而不是连接字符串中的用户 ID 和密码信息。  
  
 必须指定数据源名称如果未指定 UID、 PWD、 服务器 （或 CONNECTSTRING），和驱动程序属性。 但是，所有其他属性是可选的。 如果不指定属性，该属性默认为中的相关 DSN 选项卡指定**ODBC 数据源管理器**对话框。 属性值可能区分大小写。  
  
 连接字符串的属性如下所示：  
  
|Attribute|Description|默认值|  
|---------------|-----------------|-------------------|  
|DSN|数据源名称列出的驱动程序选项卡中**ODBC 数据源管理器**对话框。|""|  
|PWD|你想要访问 Oracle 服务器的密码。 此驱动程序支持 Oracle 对密码的限制。|""|  
|SERVER|你想要访问 Oracle 服务器的连接字符串。|""|  
|UID|Oracle 服务器用户名。 具体取决于你的系统，此属性可能不是可选 — 也就是说，某些数据库和表可能需要此属性出于安全目的。<br /><br /> 使用"/"用于 Oracle 的操作系统系统身份验证。|""|  
|BUFFERSIZE|使用在提取列时的最佳缓冲区大小。<br /><br /> 该驱动程序优化提取以便从 Oracle 服务器的一个提取返回足够的行以填充此大小的缓冲区。 较大的值往往会提高性能，如果您读取大量的数据。|65535|  
|SYNONYMCOLUMNS|当此值为 true (1)，SQLColumn （） API 调用返回列信息。 否则，SQLColumn （） 返回仅表和视图的列。 未设置此值时，用于 Oracle 的 ODBC 驱动程序将提供更快地访问。|1|  
|REMARKS|当此值为 true (1)，驱动程序返回的备注列[SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)结果集。 未设置此值时，用于 Oracle 的 ODBC 驱动程序将提供更快地访问。|0|  
|StdDayOfWeek|强制执行的 DAYOFWEEK 标量 ODBC 标准。 默认情况下，该打开的但需要本地化的版本的用户可以更改行为，以便使用 Oracle 返回任何内容。|1|  
|GuessTheColDef|指定驱动程序是否应返回为非零值*cbColDef*参数**SQLDescribeCol**。 仅适用于其中没有任何 Oracle 定义的小数位，如计算数值的列的列和列定义为数值，而无需精度或小数位数。 A **SQLDescribeCol**寻求精度返回 130 时 Oracle 不提供该信息。|0|  
  
 例如，一个连接到使用 MyOracleServerOracle Server 和 Oracle 用户 MyUserID MyDataSource 数据源的连接字符串是：  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 将连接到使用操作系统身份验证和 MyOtherOracleServerOracle 服务器 MyOtherDataSource 数据源的连接字符串：  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
