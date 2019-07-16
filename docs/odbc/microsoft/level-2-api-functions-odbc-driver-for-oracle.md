---
title: 级别 2 API 函数 （Oracle ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7600734fef44071b1f5e35c136a6b9facdb8b390
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949038"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>级别 2 API 函数（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 在此级别的函数提供级别 1 接口一致性加上额外功能，如支持书签、 动态参数和 ODBC 函数的异步执行。  
  
|API 函数|说明|  
|------------------|-----------|  
|**SQLBindParameter**|将缓冲区中的 SQL 语句的参数标记与相关联。|  
|**SQLBrowseConnect**|返回连续级别的属性和属性值。|  
|**SQLDataSources**|列出数据源名称。 实现由驱动程序管理器。|  
|**SQLDescribeParam**|返回与已准备的 SQL 语句相关联的参数标记的说明。<br /><br /> 返回最佳估计的哪些参数是，根据分析该语句。 如果参数类型不能确定，SQL_VARCHAR 返回长度为 2000年。|  
|**SQLDrivers**|实现由驱动程序管理器。|  
|**SQLExtendedFetch**|类似于**SQLFetch**但返回的每个列使用数组的多个行。 结果集是可向前滚动，并可向后滚动如果定义为静态，不只进游标。 对于只进游标与默认列绑定，从数据集大于 BUFFERSIZE 连接属性的列数据提取直接到数据缓冲区。 不支持长度可变的书签并不支持从书签提取行集 （而不是 0) 的某偏移量处。|  
|**SQLForeignKeys**|返回单个表或单个表引用其他表中的外键的列表中的外键的列表。|  
|**SQLMoreResults**|确定是否有更多结果挂起某个语句句柄，hstmt，其中包含 SELECT、 UPDATE、 INSERT 或 DELETE 语句，如果是这样，初始化这些结果的处理。<br /><br /> 使用 {resultset...} 转义序列时，oracle 支持多个结果集只能从存储过程。|  
|**SQLNativeSql**|有关使用情况的信息，请参阅[从存储过程返回数组参数](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLNumParams**|在 SQL 语句中返回参数的数目。 参数的数量应等于传递给 SQL 语句中的问号数**SQLPrepare**。|  
|**SQLPrimaryKeys**|返回包含表的主键的列名称。|  
|**SQLProcedureColumns**|返回输入和输出参数、 返回值、 一个过程，在结果集中的列和两个其他列，重载和 ORDINAL_POSITION 的列表。 重载是 Oracle 数据字典视图的 ALL_ARGUMENTS 表中的重载列。 ORDINAL_POSITION 是 Oracle 数据字典视图的 ALL_ARGUMENTS 表中的序列列。 有关打包的过程，过程名称列处于*packagename.procedurename*格式。 不返回引用的过程或函数创建同义词的过程列。|  
|**SQLProcedures**|返回数据源中的过程的列表。 有关打包的过程，过程名称列处于*packagename.procedurename*格式。<br /><br /> 因为 Oracle 不提供封装函数区分开来打包的过程的方法，该驱动程序返回 SQL_PT_UNKNOWN PROCEDURE_TYPE 列。|  
|**SQLSetPos**|设置在行集中的游标位置。 可以使用**SQLSetPos**与**SQLGetData**在行集中定位光标移到特定行后从未绑定的列中检索行。 添加到结果集中的行*fOption* SQL_ADD 添加结果集中的最后一行之后。|  
|**SQLSetScrollOptions**|设置用于控制与语句句柄，hstmt 相关联的游标的行为的选项。 有关详细信息，请参阅[游标类型和并发组合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|
