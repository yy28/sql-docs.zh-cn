---
title: 级别 1 API 函数 （Oracle ODBC 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cb1771f88987073b1ef0bcc106f8de28549affe6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085476"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>级别 1 API 函数（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 在此级别提供核心接口一致性函数加上额外功能，如事务支持。  
  
|API 函数|说明|  
|------------------|-----------|  
|**SQLColumns**|创建的结果集是指定表的列列表的表或表。 你在请求公共同义词的列时，必须已设置 SYNONYMCOLUMNS 连接属性并指定一个空字符串作为*szTableOwner*参数。 当返回的公共同义词的列，驱动程序将设置为空字符串表名称列。 结果集包含一个额外的列序号位置，在每行的结尾。 此值是表中的列的序号位置。|  
|**SQLDriverConnect**|连接到现有数据源。 有关详细信息，请参阅[连接字符串的格式和属性](../../odbc/microsoft/connection-string-format-and-attributes.md)。|  
|**SQLGetConnectOption**|返回一个连接选项的当前设置。 部分支持此函数。 该驱动程序支持的所有值*fOption*自变量，但不支持某些*vParam*值*fOption*参数[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). 有关详细信息，请参阅[连接选项](../../odbc/microsoft/connect-options.md)。|  
|**SQLGetData**|检索给定的结果集的当前记录中的单个字段的值。|  
|**SQLGetFunctions**|返回支持的所有函数，则返回 TRUE。 实现由驱动程序管理器。|  
|**SQLGetInfo**|返回信息，包括 SQLHDBC、 SQLUSMALLINT、 SQLPOINTER、 SQLSMALLINT 和 SQLSMALLINT \*，有关与连接句柄相关联的 Oracle 和数据源的 ODBC 驱动程序*hdbc*。|  
|**SQLGetStmtOption**|返回语句选项的当前设置。 有关详细信息，请参阅[语句选项](../../odbc/microsoft/statement-options.md)。|  
|**SQLGetTypeInfo**|返回有关所支持的数据源的数据类型的信息。 该驱动程序中的 SQL 结果集返回的信息。|  
|**SQLParamData**|结合使用**SQLPutData**以指定参数在语句执行时数据。|  
|**SQLPutData**|允许应用程序将参数或列的数据发送到在语句执行时驱动程序。|  
|**SQLSetConnectOption**|提供访问控制的连接方面的选项。 部分支持此函数：该驱动程序支持的所有值*fOption*自变量，但不支持某些*vParam*值*fOption*参数[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). 有关详细信息，请参阅[连接选项](../../odbc/microsoft/connect-options.md)。|  
|**SQLSetStmtOption**|设置与语句句柄，相关的选项*hstmt*。 有关详细信息，请参阅[语句选项](../../odbc/microsoft/statement-options.md)。|  
|**SQLSpecialColumns**|检索最佳列集的唯一标识表中的行。|  
|**SQLStatistics**|检索有关单个表的索引或标记名称，与表关联的统计信息的列表。 驱动程序返回的信息作为结果集。|  
|**SQLTables**|返回由参数中指定的表名称的列表**SQLTables**语句。 如果未不指定任何参数，将返回当前的数据源中存储的表名称。 驱动程序返回的信息作为结果集。<br /><br /> 枚举类型调用不会收到远程视图或本地的参数化的视图的结果集条目。 但是，调用**SQLTables**使用唯一表名称说明符将查找匹配项此类图中，如果存在具有该名称; 这使得此 API 可以检查创建的新表之前的名称冲突。<br /><br /> 公共同义词返回 TABLE_OWNER 值为""。<br /><br /> 拥有的 SYS 或系统视图都标识为系统视图。|
