---
title: 1级 API 函数（Oracle ODBC 驱动程序） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299947"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>级别 1 API 函数（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 此级别的功能提供核心接口一致性以及附加功能，例如事务支持。  
  
|API 函数|说明|  
|------------------|-----------|  
|**SQLColumns**|为表创建一个结果集，该表是指定的一个或多个表的列列表。 为公共同义词请求列时，必须设置 SYNONYMCOLUMNS 连接属性，并将空字符串指定为*szTableOwner*参数。 返回公共同义词的列时，驱动程序会将 "表名" 列设置为空字符串。 结果集在每一行的末尾包含一个附加的列序号位置。 此值是列在表中的序号位置。|  
|**SQLDriverConnect**|连接到现有数据源。 有关详细信息，请参阅[连接字符串格式和属性](../../odbc/microsoft/connection-string-format-and-attributes.md)。|  
|**SQLGetConnectOption**|返回连接选项的当前设置。 部分支持此函数。 驱动程序支持*fOption*参数的所有值，但不支持*fOption*参数[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)的某些*vParam*值。 有关详细信息，请参阅[连接选项](../../odbc/microsoft/connect-options.md)。|  
|**SQLGetData**|检索给定结果集的当前记录中的单个字段的值。|  
|**SQLGetFunctions**|对于所有支持的函数，返回 TRUE。 由驱动程序管理器实现。|  
|**SQLGetInfo**|返回有关用于 Oracle 的 ODBC 驱动程序的信息，包括 SQLHDBC、 \*SQLUSMALLINT、SQLPOINTER、SQLSMALLINT 和 SQLSMALLINT，以及与连接句柄*hdbc*关联的数据源。|  
|**SQLGetStmtOption**|返回语句选项的当前设置。 有关详细信息，请参阅[语句选项](../../odbc/microsoft/statement-options.md)。|  
|**SQLGetTypeInfo**|返回有关数据源支持的数据类型的信息。 驱动程序返回 SQL 结果集中的信息。|  
|**SQLParamData**|与**SQLPutData**结合使用，以在语句执行时指定参数数据。|  
|**SQLPutData**|允许应用程序在语句执行时向驱动程序发送参数或列的数据。|  
|**SQLSetConnectOption**|提供对管理连接各个方面的选项的访问。 此函数部分受支持：驱动程序支持*fOption*参数的所有值，但不支持*fOption*参数[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)的某些*vParam*值。 有关详细信息，请参阅[连接选项](../../odbc/microsoft/connect-options.md)。|  
|**SQLSetStmtOption**|设置与语句句柄*hstmt*相关的选项。 有关详细信息，请参阅[语句选项](../../odbc/microsoft/statement-options.md)。|  
|**SQLSpecialColumns**|检索唯一标识表中的行的一组最佳列。|  
|**SQLStatistics**|检索与表相关联的单个表和索引的统计信息列表。 驱动程序将以结果集的形式返回该信息。|  
|**SQLTables**|返回由**SQLTables**语句中的参数指定的表名称的列表。 如果未指定参数，则返回存储在当前数据源中的表名。 驱动程序将以结果集的形式返回该信息。<br /><br /> 枚举类型调用不会接收远程视图或本地参数化视图的结果集条目。 但是，使用唯一表名称说明符调用**SQLTables**将找到此类视图的匹配项（如果存在）;这允许 API 在创建新表之前检查名称冲突。<br /><br /> 使用 TABLE_OWNER 值 "" 返回公共同义词。<br /><br /> SYS 或 SYSTEM 所拥有的视图被标识为系统视图。|
