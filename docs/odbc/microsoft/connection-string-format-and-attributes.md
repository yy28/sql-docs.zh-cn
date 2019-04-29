---
title: 连接字符串的格式和属性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98c8e18432bfd386555863a917824b18b2d11885
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62902815"
---
# <a name="connection-string-format-and-attributes"></a>连接字符串格式和属性
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 而不是使用对话框中，某些应用程序可能需要一个连接字符串，指定数据源连接信息。 连接字符串由多个属性，指定驱动程序连接到数据源的方式组成。 属性用于标识特定的驱动程序需要知道来进行适当的数据源连接的信息。 每个驱动程序可能有一组不同的属性，但连接字符串的格式都始终相同。 连接字符串的格式如下：  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Microsoft ODBC Driver for Oracle 支持的驱动程序，可以使用的第一个版本的连接字符串格式`CONNECTSTRING`而不是 = `SERVER=`。  
  
 如果您要连接到的数据源提供程序支持 Windows 身份验证，则应指定`Trusted_Connection=yes`而不是在连接字符串中的用户 ID 和密码信息。  
  
 必须指定数据源，如果未指定 UID、 PWD、 服务器 （或 CONNECTSTRING），命名和驱动程序属性。 但是，所有其他属性是可选的。 如果未指定属性，该属性默认为的相关 DSN 选项卡中指定**ODBC 数据源管理器**对话框。 属性值可能区分大小写。  
  
 连接字符串的属性如下所示：  
  
|特性|Description|默认值|  
|---------------|-----------------|-------------------|  
|DSN|数据源名称中的驱动程序选项卡列出**ODBC 数据源管理器**对话框。|""|  
|PWD|你想要访问 Oracle 服务器的密码。 此驱动程序支持 Oracle 置于密码的限制。|""|  
|SERVER|你想要访问 Oracle 服务器的连接字符串。|""|  
|UID|Oracle Server 用户名。 具体取决于您的系统，此属性可能不是可有可无-也就是说，某些数据库和表可能需要此属性以安全为目的。<br /><br /> 使用"/"用于 Oracle 的操作系统系统身份验证。|""|  
|BUFFERSIZE|使用提取的列时的最佳缓冲区大小。<br /><br /> 该驱动程序可优化提取，以便从 Oracle 服务器的一个提取都将返回足够行来填充此大小的缓冲区。 较大的值往往会提高性能，如果您读取大量数据。|65535|  
|SYNONYMCOLUMNS|当此值为 true (1) 的 SQLColumn （） API 调用返回的列信息。 否则，SQLColumn （） 返回仅对表和视图的列。 Oracle ODBC 驱动程序提供更快地访问时不设置此值。|1|  
|REMARKS|当此值为 true (1)，该驱动程序返回的备注列[SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)结果集。 Oracle ODBC 驱动程序提供更快地访问时不设置此值。|0|  
|StdDayOfWeek|强制实施的 DAYOFWEEK 标量 ODBC 标准。 默认情况下，这打开的但需要本地化的版本的用户可以更改要使用 Oracle 返回任何内容的行为。|1|  
|GuessTheColDef|指定驱动程序是否应返回非零值*cbColDef*的参数**SQLDescribeCol**。 仅适用于其中没有任何 Oracle 定义的小数位，如计算数值的列的列和列定义为数值，而无需精度或小数位数。 一个**SQLDescribeCol** Oracle 不提供该信息时，调用返回 130 的精度。|0|  
  
 例如，将为连接到使用 MyOracleServerOracle Server 和 Oracle 用户 MyUserID MyDataSource 数据源的连接字符串：  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 将连接到使用操作系统身份验证和 MyOtherOracleServerOracle Server MyOtherDataSource 数据源的连接字符串：  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
