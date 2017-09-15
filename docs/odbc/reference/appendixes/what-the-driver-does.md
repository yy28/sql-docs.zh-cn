---
title: "该驱动程序的用途 |Microsoft 文档"
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
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 07e94046370f8140fdacec2cf708de0a62311a27
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="what-the-driver-does"></a>该驱动程序的用途
下表总结了哪些功能和语句属性 ODBC 3*.x*驱动程序应实现的块和可滚动的光标。  
  
|函数或<br /><br /> 语句属性|注释|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|集的行状态数组地址由填写**SQLFetch**和**SQLFetchScroll**。 此数组还由填写**SQLSetPos**如果**SQLSetPos**在语句状态 S6 中调用。 如果**SQLSetPos**称为处于状态 S7，不填充此数组但指向的数组*RowStatusArray*参数**SQLExtendedFetch**填充。 有关详细信息，请参阅[语句转换](../../../odbc/reference/appendixes/statement-transitions.md)附录 b: ODBC 状态转换表中。|  
|SQL_ATTR_ROWS_FETCHED_PTR|在其中设置缓冲区的地址**SQLFetch**和**SQLFetchScroll**返回提取的行数。 如果**SQLExtendedFetch**是调用，不填充此缓冲区但*RowCountPtr*参数指向的提取的行数。|  
|SQL_ATTR_ROW_ARRAY_SIZE|设置使用的行集大小**SQLFetch**和**SQLFetchScroll**。|  
|SQL_ROWSET_SIZE|设置使用的行集大小**SQLExtendedFetch**。 ODBC 3*.x*驱动程序实现此如果他们想要使用 ODBC 2。*x*应用程序来调用**SQLExtendedFetch**或**SQLSetPos**。|  
|**SQLBulkOperations**|如果 ODBC 3*.x*驱动程序都应适用于 ODBC 2。*x*使用的应用程序**SQLSetPos**与*操作*驱动程序必须支持的 SQL_ADD， **SQLSetPos**与*操作*的除了 SQL_ADD **SQLBulkOperations**与*操作*SQL_ADD。|  
|**SQLExtendedFetch**|返回指定的行集。 ODBC 3*.x*驱动程序实现此如果他们想要使用 ODBC 2。*x*应用程序来调用**SQLExtendedFetch**或**SQLSetPos**。 以下是实现详细信息：<br /><br /> -驱动程序从 SQL_ROWSET_SIZE 语句属性的值中检索行集大小。<br />-驱动程序检索的地址中的行状态数组*RowStatusArray*参数时，不 SQL_ATTR_ROW_STATUS_PTR 语句属性。 *RowStatusArray*对的调用中的自变量**SQLExtendedFetch**必须不能为 null 指针。 (请注意，在 ODBC 3*.x*，SQL_ATTR_ROW_STATUS_PTR 语句属性可以是 null 指针。)<br />-驱动程序检索从行提取缓冲区的地址*RowCountPtr*参数时，不 SQL_ATTR_ROWS_FETCHED_PTR 语句属性。<br />-驱动程序返回 SQLSTATE 01S01 （行中的错误） 以指示通过调用提取的行时出现了错误**SQLExtendedFetch**。 ODBC 3*.x*驱动程序应返回 SQLSTATE 01S01 （行中的错误） 时，才**SQLExtendedFetch**调用时，不时**SQLFetch**或**SQLFetchScroll**调用。 若要保留向后兼容，当 SQLSTATE 01S01 （行中的错误） 返回的**SQLExtendedFetch**，驱动程序管理器不会根据"序列的状态中所述的规则错误队列中订购状态记录记录"部分[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。|  
|**SQLFetch**|返回下一步的行集。 以下是实现详细信息：<br /><br /> -驱动程序从 SQL_ATTR_ROW_ARRAY_SIZE 语句属性的值中检索行集大小。<br />-驱动程序从 SQL_ATTR_ROW_STATUS_PTR 语句属性检索的行状态数组的地址。<br />-驱动程序检索的 SQL_ATTR_ROWS_FETCHED_PTR 语句属性中提取缓冲区的行的地址。<br />-应用程序可以混合使用之间的调用**SQLFetchScroll**和**SQLFetch**。<br />-   **SQLFetch**返回书签，如果第 0 列绑定。<br />-   **SQLFetch**可以调用以返回多个行。<br />-驱动程序不返回 SQLSTATE 01S01 （行中的错误） 以指示通过调用提取的行时出现了错误**SQLFetch**。|  
|**SQLFetchScroll**|返回指定的行集。 以下是实现详细信息：<br /><br /> -驱动程序从 SQL_ATTR_ROW_ARRAY_SIZE 语句属性中检索行集大小。<br />-驱动程序从 SQL_ATTR_ROW_STATUS_PTR 语句属性检索的行状态数组的地址。<br />-驱动程序检索的 SQL_ATTR_ROWS_FETCHED_PTR 语句属性中提取缓冲区的行的地址。<br />-应用程序可以混合使用之间的调用**SQLFetchScroll**和**SQLFetch**。<br />-驱动程序不返回 SQLSTATE 01S01 （行中的错误） 以指示通过调用提取的行时出现了错误**SQLFetchScroll**。|  
|**SQLSetPos**|执行各种定位的操作。 以下是实现详细信息：<br /><br /> -这可以语句状态 S6 或 S7 中调用。 有关更多详细信息，请参阅[语句转换](../../../odbc/reference/appendixes/statement-transitions.md)附录 b: ODBC 状态转换表中。<br />-如果这在语句状态 S5 或 S6 中调用，该驱动程序从 SQL_ATTR_ROWS_FETCHED_PTR 语句属性和 SQL_ATTR_ROW_STATUS_PTR 语句属性中的行状态数组的地址中检索行集大小。<br />-驱动程序如果这称为语句状态 S7 中，从 SQL_ROWSET_SIZE 语句属性和地址中的行状态数组中检索行集大小*RowStatusArray*参数**SQLExtendedFetch**。<br />-驱动程序返回 SQLSTATE 01S01 （行中的错误） 只是为了指示调用提取的行时出现了错误**SQLSetPos**状态 S7 中调用函数时执行大容量操作。 若要保留向后兼容性，如果 SQLSTATE 01S01 （行中的错误） 返回的**SQLSetPos**，驱动程序管理器不会根据"序列的状态记录"中所述的规则错误队列中订购状态记录部分[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。<br />-如果驱动程序应适用于 ODBC 2。*x*应用程序来调用**SQLSetPos**与*操作*SQL_ADD 自变量，该驱动程序必须支持**SQLSetPos**与*操作*SQL_ADD 自变量。|
