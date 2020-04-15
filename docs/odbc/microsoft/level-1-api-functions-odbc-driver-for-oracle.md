---
title: 1 级 API 功能（Oracle 的 ODBC 驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37305ee75ebeb0686bafe039f1102cb3c6e18674
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299947"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>级别 1 API 函数（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 此级别的功能提供核心接口一致性以及其他功能（如事务支持）。  
  
|API 功能|说明|  
|------------------|-----------|  
|**SQLColumns**|为表创建结果集，该表是指定表或表的列列表。 请求 PUBLIC 同义词的列时，必须设置 SYNONYMCOLUMNS 连接属性，并将空字符串指定为*szTableOwner*参数。 返回 PUBLIC 同义词的列时，驱动程序将 TABLE NAME 列设置为空字符串。 结果集在每行末尾包含一个附加列"ORDINAL 位置"。 此值是表中列的正位位置。|  
|**SQLDriverConnect**|连接到现有数据源。 有关详细信息，请参阅[连接字符串格式和属性](../../odbc/microsoft/connection-string-format-and-attributes.md)。|  
|**SQLGetConnectOption**|返回连接选项的当前设置。 此函数部分受支持。 驱动程序支持*fOption*参数的所有值，但不支持*fOption*参数[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)的某些*vParam*值。 有关详细信息，请参阅[连接选项](../../odbc/microsoft/connect-options.md)。|  
|**SQLGetData**|检索给定结果集的当前记录中单个字段的值。|  
|**SQLGetFunctions**|为所有支持的函数返回 TRUE。 由驱动程序管理器实施。|  
|**SQLGetInfo**|返回有关 Oracle 的 ODBC 驱动程序以及与连接句柄\**hdbc*关联的数据源的信息，包括 SQLHDBC、SQLUSMALLINT、SQLPOINTER、SQLSMALLINT 和 SQLSMALLINT。|  
|**SQLGetStmtOption**|返回语句选项的当前设置。 有关详细信息，请参阅[语句选项](../../odbc/microsoft/statement-options.md)。|  
|**SQLGetTypeInfo**|返回有关数据源支持的数据类型的信息。 驱动程序返回 SQL 结果集中的信息。|  
|**SQLParamData**|与**SQLPutData**结合使用，在语句执行时指定参数数据。|  
|**SQLPutData**|允许应用程序在语句执行时将参数或列的数据发送到驱动程序。|  
|**SQLSet 连接选项**|提供对管理连接各个方面的选项的访问。 此函数部分支持：驱动程序支持*fOption*参数的所有值，但不支持*fOption*参数[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)的某些*vParam*值。 有关详细信息，请参阅[连接选项](../../odbc/microsoft/connect-options.md)。|  
|**SQLSetStmtOption**|设置与语句句柄*hstmt*相关的选项。 有关详细信息，请参阅[语句选项](../../odbc/microsoft/statement-options.md)。|  
|**SQLSpecialColumns**|检索唯一标识表中行的最佳列集。|  
|**SQLStatistics**|检索有关单个表以及与表关联的索引或标记名称的统计信息列表。 驱动程序将返回结果集。|  
|**SQLTables**|返回**SQLTables**语句中参数指定的表名称的列表。 如果未指定参数，则返回存储在当前数据源中的表名称。 驱动程序将返回结果集。<br /><br /> 枚举类型调用将不会接收远程视图或本地参数化视图的结果集条目。 但是，对**SQLTables**的调用具有唯一的表名称指定器，将查找具有该名称的此类视图的匹配项（如果存在）;这允许 API 在创建新表之前检查名称冲突。<br /><br /> 公共同义词返回时，值为"TABLE_OWNER。<br /><br /> SYS 或 SYSTEM 拥有的视图标识为系统视图。|
