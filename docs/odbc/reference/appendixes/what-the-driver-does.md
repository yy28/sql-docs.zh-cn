---
title: 驱动程序的用途 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9a80167d00a76f667132647b3d152dda5c1a4b3
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792672"
---
# <a name="what-the-driver-does"></a>驱动程序的用途
下表总结了哪些功能和语句属性 ODBC *3.x*驱动程序应实现的块和可滚动游标。  
  
|函数或<br /><br /> 语句属性|注释|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|集由行状态数组的地址填写**SQLFetch**并**SQLFetchScroll**。 此数组还通过来填充**SQLSetPos**如果**SQLSetPos**语句状态 S6 中调用。 如果**SQLSetPos**称为在 S7 状态中，不填充此数组，但指向的数组*RowStatusArray*自变量**SQLExtendedFetch**进行填充。 有关详细信息，请参阅[语句转换](../../../odbc/reference/appendixes/statement-transitions.md)在附录 b:状态转换表。|  
|SQL_ATTR_ROWS_FETCHED_PTR|在其中设置缓冲区的地址**SQLFetch**并**SQLFetchScroll**返回提取的行数。 如果**SQLExtendedFetch**是调用，不填充此缓冲区，但*RowCountPtr*参数指向提取的行数。|  
|SQL_ATTR_ROW_ARRAY_SIZE|设置使用的行集大小**SQLFetch**并**SQLFetchScroll**。|  
|SQL_ROWSET_SIZE|设置使用的行集大小**SQLExtendedFetch**。 ODBC *3.x*如果他们想要使用 ODBC 驱动程序，则实现此*2.x*调用的应用程序**SQLExtendedFetch**或者**SQLSetPos**。|  
|**SQLBulkOperations**|如果 ODBC *3.x*驱动程序应使用 ODBC *2.x*使用的应用程序**SQLSetPos**与*操作*的 SQL_ADD，驱动程序必须支持**SQLSetPos**与*操作*的除了 SQL_ADD **SQLBulkOperations**与*操作*的 SQL添加 （_A)。|  
|**SQLExtendedFetch**|返回指定行集。 ODBC *3.x*如果他们想要使用 ODBC 驱动程序，则实现此*2.x*调用的应用程序**SQLExtendedFetch**或者**SQLSetPos**。 以下是实现详细信息：<br /><br /> -驱动程序从 SQL_ROWSET_SIZE 语句属性的值中检索行集大小。<br />-驱动程序检索的行状态数组，从地址*RowStatusArray*参数时，不将 SQL_ATTR_ROW_STATUS_PTR 语句属性。 *RowStatusArray*调用中的参数**SQLExtendedFetch**必须不能为 null 指针。 (请注意，在 ODBC *3.x*，SQL_ATTR_ROW_STATUS_PTR 语句属性可以为 null 指针。)<br />-驱动程序检索中的行提取缓冲区的地址*RowCountPtr*参数时，不将 SQL_ATTR_ROWS_FETCHED_PTR 语句属性。<br />-驱动程序将返回 SQLSTATE 01S01 （行中的错误） 以指示错误发生时通过调用提取的行**SQLExtendedFetch**。 ODBC *3.x*驱动程序应返回 SQLSTATE 01S01 （行中的错误） 时，才**SQLExtendedFetch**调用时，不时**SQLFetch**或**SQLFetchScroll**调用。 若要保留向后兼容，当 SQLSTATE 01S01 （行中的错误） 返回的**SQLExtendedFetch**，驱动程序管理器不会根据"序列的状态中所述的规则，错误队列中进行排序状态记录记录"部分[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。|  
|**SQLFetch**|返回下一步的行集。 以下是实现详细信息：<br /><br /> -驱动程序从 SQL_ATTR_ROW_ARRAY_SIZE 语句属性的值中检索行集大小。<br />-驱动程序从 SQL_ATTR_ROW_STATUS_PTR 语句属性检索的行状态数组的地址。<br />-驱动程序检索从 SQL_ATTR_ROWS_FETCHED_PTR 语句属性提取缓冲区行的地址。<br />-应用程序可以混合使用之间的调用**SQLFetchScroll**并**SQLFetch**。<br />-   **SQLFetch**如果绑定列 0，则返回的书签。<br />-   **SQLFetch**可以调用以返回多个行。<br />-驱动程序不会返回 SQLSTATE 01S01 （行中的错误） 以指示错误发生时通过调用提取的行**SQLFetch**。|  
|**SQLFetchScroll**|返回指定行集。 以下是实现详细信息：<br /><br /> -驱动程序从 SQL_ATTR_ROW_ARRAY_SIZE 语句属性中检索行集大小。<br />-驱动程序从 SQL_ATTR_ROW_STATUS_PTR 语句属性检索的行状态数组的地址。<br />-驱动程序检索从 SQL_ATTR_ROWS_FETCHED_PTR 语句属性提取缓冲区行的地址。<br />-应用程序可以混合使用之间的调用**SQLFetchScroll**并**SQLFetch**。<br />-驱动程序不会返回 SQLSTATE 01S01 （行中的错误） 以指示错误发生时通过调用提取的行**SQLFetchScroll**。|  
|**SQLSetPos**|执行各种定位的操作。 以下是实现详细信息：<br /><br /> -这可调用语句状态 S6 或 S7 中。 有关更多详细信息，请参阅[语句转换](../../../odbc/reference/appendixes/statement-transitions.md)在附录 b:状态转换表。<br />-如果这在语句状态 S5 或 S6 中调用，该驱动程序检索行集大小从 SQL_ATTR_ROWS_FETCHED_PTR 语句属性和行状态数组从 SQL_ATTR_ROW_STATUS_PTR 语句属性的地址。<br />-该驱动程序如果这在语句的状态 S7 中调用，从 SQL_ROWSET_SIZE 语句属性和行状态数组，从地址中检索行集大小*RowStatusArray*自变量的**SQLExtendedFetch**。<br />-驱动程序将返回 SQLSTATE 01S01 （行中的错误） 仅以指示错误发生时通过调用提取的行**SQLSetPos**在 S7 状态中调用该函数时执行大容量操作。 若要保留向后兼容性，如果 SQLSTATE 01S01 （行中的错误） 返回的**SQLSetPos**，驱动程序管理器不会根据序列的状态"记录"中所述的规则，错误队列中进行排序状态记录部分[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。<br />-如果驱动程序应使用 ODBC *2.x*调用的应用程序**SQLSetPos**与*操作*SQL_ADD 参数，该驱动程序必须支持**SQLSetPos**与*操作*SQL_ADD 参数。|
