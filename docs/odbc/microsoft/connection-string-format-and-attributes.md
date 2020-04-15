---
title: 连接字符串格式和属性 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d95866976d2e83c058f83b3a0ae5e9a4e8888ed1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281147"
---
# <a name="connection-string-format-and-attributes"></a>连接字符串格式和属性
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 某些应用程序可能需要指定数据源连接信息的连接字符串，而不是使用对话框。 连接字符串由许多属性组成，这些属性指定驱动程序如何连接到数据源。 属性标识驱动程序在建立适当的数据源连接之前需要知道的特定信息段。 每个驱动程序可能具有一组不同的属性，但连接字符串格式始终相同。 连接字符串具有以下格式：  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Oracle 的 Microsoft ODBC 驱动程序支持驱动程序的第一个版本的连接字符串格式，该驱动程序使用`CONNECTSTRING`=`SERVER=`而不是 。  
  
 如果要连接到支持 Windows 身份验证的数据源提供程序，则应在连接字符串中指定`Trusted_Connection=yes`而不是用户 ID 和密码信息。  
  
 如果不指定 UID、PWD、SERVER（或 CONNECTSTRING）和 DRIVER 属性，则必须指定数据源名称。 但是，所有其他属性都是可选的。 如果不指定属性，该属性默认为**ODBC 数据源管理员**对话框的相关 DSN 选项卡中指定的属性。 属性值可能区分大小写。  
  
 连接字符串的属性如下所示：  
  
|特性|描述|默认值|  
|---------------|-----------------|-------------------|  
|DSN|**ODBC 数据源管理员**对话框的"驱动程序"选项卡中列出的数据源名称。|""|  
|PWD|要访问的 Oracle 服务器的密码。 此驱动程序支持 Oracle 对密码的限制。|""|  
|SERVER|要访问的 Oracle 服务器的连接字符串。|""|  
|UID|Oracle 服务器用户名。 根据您的系统，此属性可能不是可选的 - 也就是说，出于安全目的，某些数据库和表可能需要此属性。<br /><br /> 使用"/"使用 Oracle 的操作系统身份验证。|""|  
|缓冲区大小|提取列时使用的最佳缓冲区大小。<br /><br /> 驱动程序优化提取，以便从 Oracle 服务器提取的行返回足够的行来填充此大小的缓冲区。 如果获取大量数据，则值越大，性能也会提高。|65535|  
|同义词|当此值为 true （1）时，SQLColumn（ ） API 调用将返回列信息。 否则，SQLColumn（ ） 仅返回表和视图的列。 未设置此值时，Oracle 的 ODBC 驱动程序可提供更快的访问。|1|  
|REMARKS|当此值为 true （1）时，驱动程序返回[SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)结果集的备注列。 未设置此值时，Oracle 的 ODBC 驱动程序可提供更快的访问。|0|  
|斯特德日周|为"天天"标量强制实施 ODBC 标准。 默认情况下，这已打开，但需要本地化版本的用户可以更改行为以使用 Oracle 返回的任何内容。|1|  
|猜谜|指定驱动程序是否应返回**SQLDescribeCol**的*cbColDef*参数的非零值。 仅适用于没有 Oracle 定义比例的列，例如计算的数字列和定义为 NUMBER 的列，而不具有精度或比例。 当 Oracle 不提供该信息时 **，SQLDescribeCol**调用返回 130 的精度。|0|  
  
 例如，使用 MyOracleServerOracle 服务器和 Oracle 用户 MyUserID 连接到 MyDataSource 数据源的连接字符串是：  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 使用操作系统身份验证和 MyOtherOracleServerOracle 服务器连接到 MyOtherDataSource 数据源的连接字符串是：  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
