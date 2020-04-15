---
title: 2 级 API 功能（Oracle 的 ODBC 驱动程序） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284177"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>级别 2 API 函数（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 此级别的函数提供 1 级接口一致性以及其他功能，如支持书签、动态参数和异步执行 ODBC 函数。  
  
|API 功能|说明|  
|------------------|-----------|  
|**SQLBindParameter**|将缓冲区与 SQL 语句中的参数标记关联。|  
|**SQLBrowseConnect**|返回属性和属性值的连续级别。|  
|**SQLData源**|列出数据源名称。 由驱动程序管理器实施。|  
|**SQLDescribeParam**|返回与准备好的 SQL 语句关联的参数标记的说明。<br /><br /> 返回基于分析语句的参数的最佳猜测。 如果无法确定参数类型，SQL_VARCHAR返回长度为 2000。|  
|**SQLDrivers**|由驱动程序管理器实施。|  
|**SQL 扩展获取**|与**SQLFetch**类似，但使用每个列的数组返回多行。 结果集是可向前滚动的，如果游标定义为静态的，而不是仅向前滚动，则可以向后滚动。 对于具有默认列绑定的仅转发游标，大于 BUFFERSIZE 连接属性的数据集的列数据将直接提取到数据缓冲区中。 不支持可变长度书签，不支持从书签的偏移量（0 以外的）提取行集。|  
|**SQLForeignKeys**|返回单个表中的外键列表，或引用单个表的其他表中的外键列表。|  
|**SQLMoreResults**|确定语句句柄（hstmt）上是否挂起更多结果，其中包含 SELECT、更新、插入或 DELETE 语句，如果是，则初始化这些结果的处理。<br /><br /> 当使用 _结果集...|  
|**SQLNativeSql**|有关使用情况的信息，请参阅[从存储过程返回数组参数](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLNumParams**|返回 SQL 语句中的参数数。 参数数应等于传递给**SQLPrepare**的 SQL 语句中的问号数。|  
|**SQLPrimaryKeys**|返回构成表主键的列名称。|  
|**SQLProcedureColumns**|返回输入和输出参数的列表、返回值、单个过程的结果集中的列以及另外两列"重载"和"ORDINAL_POSITION。 "重"是 Oracle 数据字典视图ALL_ARGUMENTS表中的"重载"列。 ORDINAL_POSITION是 Oracle 数据字典视图ALL_ARGUMENTS表中的 SEQUENCE 列。 对于打包过程，程序名称列采用*包名.程序名称*格式。 不返回引用过程或函数的已创建同义词的过程列。|  
|**SQLProcedures**|返回数据源中的过程列表。 对于打包过程，程序名称列采用*包名.程序名称*格式。<br /><br /> 由于 Oracle 不提供区分打包过程和打包函数的方法，因此驱动程序返回PROCEDURE_TYPE列SQL_PT_UNKNOWN。|  
|**SQLSetPos**|设置行集中的光标位置。 您可以将游标定位到行集中的特定行后，将**SQLSetPos**与**SQLGetData**一起从未绑定列中检索行。 使用*fOption* SQL_ADD添加到结果集的行在结果集中的最后一行之后添加。|  
|**SQLSetScroll 选项**|设置控制与语句句柄 hstmt 关联的游标行为的选项。 有关详细信息，请参阅[光标类型和并发组合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|
