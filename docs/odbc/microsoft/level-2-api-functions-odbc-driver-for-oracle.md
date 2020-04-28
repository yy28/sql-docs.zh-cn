---
title: 2级 API 函数（Oracle ODBC 驱动程序） |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1e181c5863d6b906eaf9a3ba499728c595f0449
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284177"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>级别 2 API 函数（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 此级别的函数提供1级接口一致性以及附加功能，例如支持书签、动态参数和 ODBC 函数的异步执行。  
  
|API 函数|说明|  
|------------------|-----------|  
|**SQLBindParameter**|将缓冲区与 SQL 语句中的参数标记相关联。|  
|**SQLBrowseConnect**|返回属性和属性值的连续级别。|  
|**SQLDataSources**|列出数据源名称。 由驱动程序管理器实现。|  
|**SQLDescribeParam**|返回与已准备的 SQL 语句关联的参数标记的说明。<br /><br /> 基于分析语句，返回参数的最佳推测。 如果无法确定参数类型，SQL_VARCHAR 将返回，长度为2000。|  
|**SQLDrivers**|由驱动程序管理器实现。|  
|**SQLExtendedFetch**|类似于**SQLFetch** ，但使用每个列的数组返回多个行。 如果将游标定义为静态而不是只进，则结果集是可向前滚动的，并且可向后滚动。 对于带有默认列绑定的只进游标，将直接在数据缓冲区中提取数据集中大于 BUFFERSIZE 连接属性的列数据。 不支持可变长度书签，而且不支持从书签提取偏移量（0除外）的行集。|  
|**SQLForeignKeys**|返回单个表中的外键列表，或引用单个表的其他表中的外键列表。|  
|**SQLMoreResults**|确定对于包含 SELECT、UPDATE、INSERT 或 DELETE 语句的语句句柄（hstmt）是否挂起更多结果，如果是，则为这些结果初始化处理。<br /><br /> 使用 {resultset ...} 转义序列时，Oracle 仅在存储过程中支持多个结果集。|  
|**SQLNativeSql**|有关使用情况的信息，请参阅[从存储过程返回数组参数](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLNumParams**|返回 SQL 语句中参数的数目。 参数的数目应等于传递给**SQLPrepare**的 SQL 语句中的问号数。|  
|**SQLPrimaryKeys**|返回构成表的主键的列名称。|  
|**SQLProcedureColumns**|返回一个列表，其中列出了输入和输出参数、返回值、单个过程的结果集中的列、重载和 ORDINAL_POSITION 两个其他列。 重载是来自 Oracle 数据字典视图 ALL_ARGUMENTS 表的重载列。 ORDINAL_POSITION 是 Oracle 数据字典视图的 ALL_ARGUMENTS 表中的序列列。 对于打包过程，过程名称列的格式为*packagename。* 不返回引用过程或函数的已创建同义词的过程列。|  
|**SQLProcedures**|返回数据源中的过程列表。 对于打包过程，过程名称列的格式为*packagename。*<br /><br /> 由于 Oracle 不提供一种方式来区分打包的函数的打包过程，因此该驱动程序将为 PROCEDURE_TYPE 列返回 SQL_PT_UNKNOWN。|  
|**SQLSetPos**|设置行集中的光标位置。 将游标定位到行集中的特定行后，可以使用**SQLSetPos**与**SQLGetData**从未绑定的列中检索行。 使用*fOption* SQL_ADD 添加到结果集中的行将添加到结果集中的最后一行之后。|  
|**SQLSetScrollOptions**|设置控制与语句句柄 hstmt 关联的游标的行为的选项。 有关详细信息，请参阅[游标类型和并发组合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|
