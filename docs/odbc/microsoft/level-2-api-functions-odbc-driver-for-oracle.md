---
title: "级别 2 API 函数 （适用于 Oracle 的 ODBC 驱动程序） |Microsoft 文档"
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
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb35e0e2dde90261e913ffd9ba3dc28e5859e012
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>级别 2 API 函数 （适用于 Oracle 的 ODBC 驱动程序）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 级别 1 接口一致性加上其他功能，例如支持书签、 动态参数和 ODBC 函数的异步执行，将提供此级别的函数。  
  
|API 函数|说明|  
|------------------|-----------|  
|**SQLBindParameter**|将缓冲区中的 SQL 语句的参数标记与相关联。|  
|**SQLBrowseConnect**|返回属性和属性值的连续的级别。|  
|**SQLDataSources**|列出数据源名称。 由驱动程序管理器中实现。|  
|**SQLDescribeParam**|返回与已准备的 SQL 语句关联的参数标记的说明。<br /><br /> 返回哪些参数的基于分析该语句是最佳的猜测。 如果无法确定参数类型，SQL_VARCHAR 返回长度 2000年。|  
|**SQLDrivers**|由驱动程序管理器中实现。|  
|**SQLExtendedFetch**|类似于**SQLFetch**但返回为每一列使用数组的多个行。 结果集是可向前滚动，并可向后滚动如果定义为静态、 不只进游标。 为默认列绑定使用的只进游标，从数据集大于 BUFFERSIZE 连接属性的列数据提取直接在数据缓冲区中。 不支持可变长度书签并不支持从书签中提取行集 （0) 以外的某个偏移量上。|  
|**SQLForeignKeys**|单个表或到单个表，请参阅其他表中的外键的列表中返回外键的列表。|  
|**SQLMoreResults**|确定是否更多结果处于挂起状态在语句句柄，hstmt，其中包含 SELECT、 UPDATE、 INSERT、 或 DELETE 语句，并且如果是这样，初始化这些结果的处理。<br /><br /> Oracle 支持只能从存储过程的多个结果集时使用 {resultset...} 转义序列。|  
|**SQLNativeSql**|有关用法的信息，请参阅[从存储过程返回数组参数](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLNumParams**|在 SQL 语句中返回参数的数目。 参数的数目应等于传递给 SQL 语句中的问号数**SQLPrepare**。|  
|**SQLPrimaryKeys**|返回构成表的主键的列名称。|  
|**SQLProcedureColumns**|返回输入和输出参数、 返回值、 一个单一过程中，结果集中的列和两个其他列，重载和 ORDINAL_POSITION 的列表。 重载是 Oracle 数据字典视图的 ALL_ARGUMENTS 表中的重载列。 ORDINAL_POSITION 是从 Oracle 数据字典视图的 ALL_ARGUMENTS 表序列列。 有关打包过程，过程名称列位于*packagename.procedurename*格式。 不返回指一个过程或函数的创建同义词的过程列。|  
|**SQLProcedures**|返回数据源中的过程的列表。 有关打包过程，过程名称列位于*packagename.procedurename*格式。<br /><br /> 因为 Oracle 不提供一种区分打包的过程从打包函数方法，该驱动程序返回 SQL_PT_UNKNOWN PROCEDURE_TYPE 列。|  
|**SQLSetPos**|设置在行集中的光标位置。 你可以使用**SQLSetPos**与**SQLGetData**行集合中定位光标所在位置到特定行后从未绑定的列中检索行。 添加到使用的结果集中的行*fOption* SQL_ADD 添加结果集中的最后一行之后。|  
|**SQLSetScrollOptions**|设置控制游标语句句柄，hstmt 与关联的行为的选项。 有关详细信息，请参阅[游标类型和并发组合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|

