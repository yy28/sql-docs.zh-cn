---
title: "级别 1 API 函数 （适用于 Oracle 的 ODBC 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3cd7f827ecfc367536654b9ad825302f4dba9fcf
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>级别 1 API 函数 （适用于 Oracle 的 ODBC 驱动程序）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 在此级别提供核心接口支持的函数和其他功能，例如事务支持。  
  
|API 函数|说明|  
|------------------|-----------|  
|**SQLColumns**|创建一个结果集是指定表的列列表的表或表。 你在请求公共同义词的列时，必须已设置 SYNONYMCOLUMNS 连接属性并指定一个空字符串作为*szTableOwner*自变量。 时返回的公共同义词的列，该驱动程序会将表名称列设置为一个空字符串。 结果集包含一个额外的列序号位置，在每行末尾的位置。 此值为表中的列的序号位置。|  
|**SQLDriverConnect**|连接到现有的数据源。 有关详细信息，请参阅[连接字符串格式和属性](../../odbc/microsoft/connection-string-format-and-attributes.md)。|  
|**SQLGetConnectOption**|返回连接选项的当前设置。 部分支持此功能。 驱动程序支持的所有值*fOption*自变量，但不支持某些*vParam*值*fOption*参数[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). 有关详细信息，请参阅[连接选项](../../odbc/microsoft/connect-options.md)。|  
|**SQLGetData**|检索给定的结果集的当前记录中的单个字段的值。|  
|**SQLGetFunctions**|返回适用于所有支持的函数。 由驱动程序管理器中实现。|  
|**SQLGetInfo**|返回信息，包括 SQLHDBC、 SQLUSMALLINT、 SQLPOINTER、 SQLSMALLINT 和 SQLSMALLINT \*，有关 ODBC Driver for Oracle 和数据源连接句柄，与关联*hdbc*。|  
|**SQLGetStmtOption**|返回语句选项的当前设置。 有关详细信息，请参阅[语句选项](../../odbc/microsoft/statement-options.md)。|  
|**SQLGetTypeInfo**|返回有关所支持的数据源的数据类型信息。 该驱动程序 SQL 结果集中返回的信息。|  
|**SQLParamData**|结合使用**SQLPutData**以指定在语句执行时的参数数据。|  
|**SQLPutData**|允许应用程序将参数或列的数据发送到在语句执行时驱动程序。|  
|**SQLSetConnectOption**|提供访问控制方面的连接的选项。 此函数支持部分： 驱动程序支持的所有值*fOption*自变量，但不支持某些*vParam*值*fOption*自变量[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)。 有关详细信息，请参阅[连接选项](../../odbc/microsoft/connect-options.md)。|  
|**SQLSetStmtOption**|设置与语句句柄，相关选项*hstmt*。 有关详细信息，请参阅[语句选项](../../odbc/microsoft/statement-options.md)。|  
|**SQLSpecialColumns**|检索列的最佳唯一标识表中的行集。|  
|**SQLStatistics**|检索有关单个表的索引或标记名称，与该表关联的统计信息列表。 驱动程序返回信息作为结果集。|  
|**SQLTables**|返回由参数中指定的表名称的列表**SQLTables**语句。 如果未不指定任何参数，则返回当前的数据源中存储的表名称。 驱动程序返回信息作为结果集。<br /><br /> 枚举类型调用不会收到远程视图或本地的参数化的视图的结果集条目。 但是，对的调用**SQLTables**使用唯一表名称说明符将找到匹配项对于此类视图中，如果存在，具有该名称; 这样，要检查之前创建的新表的名称冲突的 API。<br /><br /> 公共同义词返回 TABLE_OWNER 值为""。<br /><br /> 视图归 SYS 或系统被标识为系统视图。|

