---
title: 连接字符串格式和属性 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281147"
---
# <a name="connection-string-format-and-attributes"></a>连接字符串格式和属性
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 某些应用程序可能需要指定数据源连接信息的连接字符串，而不是使用对话框。 连接字符串由多个属性组成，它们指定了驱动程序连接到数据源的方式。 属性标识了驱动程序在可以进行适当的数据源连接之前需要了解的特定信息。 每个驱动程序可能有一组不同的属性，但连接字符串格式始终相同。 连接字符串具有以下格式：  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Microsoft ODBC Driver for Oracle 支持使用`CONNECTSTRING`= 而不是的`SERVER=`第一个版本的驱动程序的连接字符串格式。  
  
 如果要连接到支持 Windows 身份验证的数据源提供程序，应在连接`Trusted_Connection=yes`字符串中指定而不是用户 ID 和密码信息。  
  
 如果未指定 UID、PWD、SERVER （或 CONNECTSTRING）以及驱动程序属性，则必须指定数据源名称。 但是，所有其他属性都是可选的。 如果未指定属性，则该属性默认为在 " **ODBC 数据源管理器**" 对话框的 "相关 DSN" 选项卡中指定的属性。 属性值可能区分大小写。  
  
 连接字符串的属性如下所示：  
  
|特性|描述|默认值|  
|---------------|-----------------|-------------------|  
|DSN|" **ODBC 数据源管理器**" 对话框的 "驱动程序" 选项卡中列出的数据源名称。|""|  
|PWD|要访问的 Oracle 服务器的密码。 此驱动程序支持 Oracle 置于密码中的限制。|""|  
|SERVER|要访问的 Oracle 服务器的连接字符串。|""|  
|UID|Oracle 服务器用户名。 此属性可能不是可选的，具体取决于您的系统，此属性可能会出于安全目的而需要此属性。<br /><br /> 使用 "/" 来使用 Oracle 的操作系统身份验证。|""|  
|BUFFERSIZE|提取列时使用的最佳缓冲区大小。<br /><br /> 驱动程序会优化提取，以便从 Oracle 服务器提取一次，以填充此大小的缓冲区。 如果提取大量数据，更大的值通常会提高性能。|65535|  
|SYNONYMCOLUMNS|如果此值为 true （1），则 SQLColumn （） API 调用返回列信息。 否则，SQLColumn （）仅返回表和视图的列。 如果未设置此值，则用于 Oracle 的 ODBC 驱动程序可提供更快的访问。|1|  
|REMARKS|如果此值为 true （1），则驱动程序将返回[SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)结果集的备注列。 如果未设置此值，则用于 Oracle 的 ODBC 驱动程序可提供更快的访问。|0|  
|StdDayOfWeek|强制执行 DAYOFWEEK 标量的 ODBC 标准。 默认情况下，此功能处于打开状态，但需要本地化版本的用户可以将行为更改为使用 Oracle 返回的任何内容。|1|  
|GuessTheColDef|指定驱动程序是否应为**SQLDescribeCol**的*cbColDef*参数返回非零值。 仅适用于没有 Oracle 定义的刻度的列，例如，计算所得的数值列和定义为数值的列，无精度或小数位数。 当 Oracle 不提供该信息时， **SQLDescribeCol**调用返回130的精度。|0|  
  
 例如，使用 MyOracleServerOracle 服务器和 Oracle 用户 MyUserID 连接到 MyDataSource 数据源的连接字符串应为：  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 使用操作系统身份验证和 MyOtherOracleServerOracle 服务器连接到 MyOtherDataSource 数据源的连接字符串应为：  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
