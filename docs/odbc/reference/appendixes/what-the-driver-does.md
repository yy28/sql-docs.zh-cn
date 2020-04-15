---
title: 驱动程序的作用 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0438478f5aa625ffdd4d3bcd1c0a6f0f80d3367
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301388"
---
# <a name="what-the-driver-does"></a>驱动程序的用途
下表总结了 ODBC *3.x*驱动程序应该为块和可滚动游标实现的功能和语句属性。  
  
|功能或<br /><br /> 语句属性|注释|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|设置由**SQLFetch**和**SQLFetchScroll**填充的行状态数组的地址。 如果在语句状态 S6 中调用**SQLSetPos，** 则**SQLSetPos**也会填充此数组。 如果在状态 S7 中调用**SQLSetPos，** 则此数组不会填充，但**SQL 扩展Fetch**的*RowStatusArray*参数指向的数组将填充。 有关详细信息，请参阅附录 B[中的语句转换](../../../odbc/reference/appendixes/statement-transitions.md)：ODBC 状态转换表。|  
|SQL_ATTR_ROWS_FETCHED_PTR|设置**SQLFetch**和**SQLFetchScroll**返回提取的行数的缓冲区的地址。 如果调用**SQLExtendedFetch，** 则不会填充此缓冲区，但*RowCountPtr*参数指向获取的行数。|  
|SQL_ATTR_ROW_ARRAY_SIZE|设置**SQLFetch**和**SQLFetchScroll**使用的行集大小。|  
|SQL_ROWSET_SIZE|设置**SQL 扩展获取**使用的行集大小。 如果 ODBC *3.x*驱动程序想要与调用**SQLExtendedFetch**或**SQLSetPos**的 ODBC *2.x*应用程序一起工作，则实现此目的。|  
|**SQLBulk 操作**|如果 ODBC *3.x*驱动程序应与使用**SQLSetPos**的具有SQL_ADD操作的 ODBC *2.x*应用程序一*起工作*，则驱动程序除了使用 SQL_ADD*操作*的**SQLBulk 操作**外，还必须支持具有SQL_ADD*操作*的**SQLSetPos。**|  
|**SQL 扩展获取**|返回指定的行集。 如果 ODBC *3.x*驱动程序想要与调用**SQLExtendedFetch**或**SQLSetPos**的 ODBC *2.x*应用程序一起工作，则实现此目的。 以下是实现详细信息：<br /><br /> - 驱动程序从SQL_ROWSET_SIZE语句属性的值检索行集大小。<br />- 驱动程序从*RowStatusArray*参数检索行状态数组的地址，而不是SQL_ATTR_ROW_STATUS_PTR语句属性。 对**SQL 扩展获取**的调用中的*RowStatusArray*参数不能为空指针。 （请注意，在 ODBC *3.x*中，SQL_ATTR_ROW_STATUS_PTR 语句属性可以是空指针。<br />- 驱动程序从*RowCountPtr*参数检索行获取缓冲区的地址，而不是SQL_ATTR_ROWS_FETCHED_PTR语句属性。<br />- 驱动程序返回 SQLSTATE 01S01（行中的错误），以指示在调用**SQLExtendedFetch**获取行时发生了错误。 ODBC *3.x*驱动程序应仅在调用**SQLAtFetch**时返回 SQLSTATE 01S01（行中的错误），而不是调用**SQLFetch**或**SQLFetchScroll**时返回 SQLSTATE 01S01（行中的错误）。 为了保持向后兼容性，当 SQLAaS01（行中的错误）由**SQLExtendedFetch**返回时，驱动程序管理器不会根据[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)的"状态记录序列"部分中所述的规则对错误队列中的状态记录进行排序。|  
|**SQLFetch**|返回下一个行集。 以下是实现详细信息：<br /><br /> - 驱动程序从SQL_ATTR_ROW_ARRAY_SIZE语句属性的值检索行集大小。<br />- 驱动程序从SQL_ATTR_ROW_STATUS_PTR语句属性检索行状态数组的地址。<br />- 驱动程序从SQL_ATTR_ROWS_FETCHED_PTR语句属性检索行提取缓冲区的地址。<br />- 应用程序可以在**SQLFetchScroll**和**SQLFetch**之间混合调用。<br />-   如果绑定列**0，SQLFetch**将返回书签。<br />-   可以调用**SQLFetch**来返回多行。<br />- 驱动程序不返回 SQLSTATE 01S01（行中的错误），以指示在调用**SQLFetch**获取行时发生了错误。|  
|**SQLFetchScroll**|返回指定的行集。 以下是实现详细信息：<br /><br /> - 驱动程序从SQL_ATTR_ROW_ARRAY_SIZE语句属性检索行集大小。<br />- 驱动程序从SQL_ATTR_ROW_STATUS_PTR语句属性检索行状态数组的地址。<br />- 驱动程序从SQL_ATTR_ROWS_FETCHED_PTR语句属性检索行提取缓冲区的地址。<br />- 应用程序可以在**SQLFetchScroll**和**SQLFetch**之间混合调用。<br />- 驱动程序不返回 SQLSTATE 01S01（行中的错误），以指示在调用**SQLFetchScroll**获取行时发生了错误。|  
|**SQLSetPos**|执行各种定位操作。 以下是实现详细信息：<br /><br /> - 这可以在语句状态 S6 或 S7 中调用。 有关详细信息，请参阅附录 B[中的语句转换](../../../odbc/reference/appendixes/statement-transitions.md)：ODBC 状态转换表。<br />- 如果在语句状态 S5 或 S6 中调用此选项，驱动程序将从SQL_ATTR_ROWS_FETCHED_PTR语句属性和行状态数组的地址从SQL_ATTR_ROW_STATUS_PTR语句属性中检索行集大小。<br />- 如果在语句状态 S7 中调用此选项，驱动程序将从 SQL_ROWSET_SIZE 语句属性和从**SQL 延长获取**的*RowStatusArray*参数中检索行集大小。<br />- 驱动程序返回 SQLSTATE 01S01（行中的错误），只是为了指示在调用**SQLSetPos**以在状态 S7 中调用函数时获取行以执行批量操作时发生了错误。 为了保持向后兼容性，如果**SQLSetPos**返回 SQLSTATE 01S01（行中的错误），驱动程序管理器不会根据[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)的"状态记录序列"部分中所述的规则对错误队列中的状态记录进行排序。<br />- 如果驱动程序应使用调用**SQLSetPos**的 ODBC *2.x*应用程序，*操作*参数为 SQL_ADD，则驱动程序必须支持**SQLSetPos，***操作*参数为 SQL_ADD。|
