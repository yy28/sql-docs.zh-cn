---
title: "驱动程序管理器会 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver manager [ODBC], backward compatibility
- compatibility [ODBC], driver manager
- ODBC driver manager [ODBC]
- backward compatibility [ODBC], driver manager
ms.assetid: 57f65c38-d9ee-46c8-9051-128224a582c6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64c6fb04fe5c5c693da4982e1c12194bc7e42f98
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="what-the-driver-manager-does"></a>驱动程序管理器的用途
下表总结了如何 ODBC 3*.x*驱动程序管理器将调用映射到 ODBC 2。*x*和 ODBC 3*.x*驱动程序。  
  
|函数或<br /><br /> 语句属性|注释|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向该书签用于**SQLFetchScroll**。 以下是实现详细信息：<br /><br /> -如果应用程序设置此 ODBC 2 中。*x*驱动程序，ODBC 3*.x*驱动程序管理器对其进行缓存。 它取消引用指针，并将值传递给 ODBC 2。*x*中的驱动程序*FetchOffset*参数**SQLExtendedFetch**时**SQLFetchScroll**应用程序更高版本调用。<br />-应用程序如果 ODBC 3 中设置此*.x*驱动程序，ODBC 3*.x*驱动程序管理器将传递到该驱动程序的调用。|  
|SQL_ATTR_ROW_STATUS_PTR|指向行状态数组由填写**SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，和**SQLSetPos**。 以下是实现详细信息：<br /><br /> -如果应用程序设置此 ODBC 2 中。*x*驱动程序，ODBC 3*.x*驱动程序管理器缓存其值。 它将此值传递到 ODBC 2。*x*中的驱动程序*RowStatusArray*参数**SQLExtendedFetch**时**SQLFetchScroll**或**SQLFetch**调用。<br />-应用程序如果 ODBC 3 中设置此*.x*驱动程序，ODBC 3*.x*驱动程序管理器将传递到该驱动程序的调用。<br />-在状态 S6，如果应用程序将 SQL_ATTR_ROW_STATUS_PTR，然后调用**SQLBulkOperations** (与*操作*的 SQL_ADD) 或**SQLSetPos**而无需首先调用**SQLFetch**或**SQLFetchScroll**，SQLSTATE HY011 （不能设置属性现在） 返回。|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向在其中缓冲区**SQLFetch**和**SQLFetchScroll**返回提取的行数。 以下是实现详细信息：<br /><br /> -如果应用程序设置此 ODBC 2 中。*x*驱动程序，ODBC 3*.x*驱动程序管理器缓存其值。 它将此值传递到 ODBC 2。*x*中的驱动程序*RowCountPtr*参数**SQLExtendedFetch**时**SQLFetch**或**SQLFetchScroll**应用程序调用。<br />-应用程序如果 ODBC 3 中设置此*.x*驱动程序，ODBC 3*.x*驱动程序管理器将传递到该驱动程序的调用。|  
|SQL_ATTR_ROW_ARRAY_SIZE|设置行集大小。 以下是实现详细信息：<br /><br /> -如果应用程序设置此 ODBC 2 中。*x*驱动程序，ODBC 3*.x*驱动程序管理器将其映射到 SQL_ROWSET_SIZE 语句属性。<br />-应用程序如果 ODBC 3 中设置此*.x*驱动程序，ODBC 3*.x*驱动程序管理器将传递到该驱动程序的调用。<br />-当应用程序使用 ODBC 3*.x*驱动程序调用**SQLSetScrollOptions**，SQL_ROWSET_SIZE 设置中的值为*RowsetSize*参数如果基础驱动程序不支持**SQLSetScrollOptions**。|  
|SQL_ROWSET_SIZE|设置使用的行集大小**SQLExtendedFetch**时**SQLExtendedFetch**由 ODBC 2*.x*应用程序。 以下是实现详细信息：<br /><br /> -如果应用程序将设置此操作，请 ODBC 3*.x*驱动程序管理器将传递到该驱动程序，而不考虑驱动程序版本的调用。<br />-当应用程序使用 ODBC 2。*x*驱动程序调用**SQLSetScrollOptions**，SQL_ROWSET_SIZE 设置中的值为**RowsetSize**自变量。|  
|**SQLBulkOperations**|执行插入操作或更新，删除或由书签操作的提取。 以下是实现详细信息：<br /><br /> -如果应用程序调用**SQLBulkOperations**与*操作*的 ODBC 2 中的 SQL_ADD。*x*驱动程序，ODBC 3*.x*驱动程序管理器将其映射到**SQLSetPos**与*操作*SQL_ADD。<br />-当使用 ODBC 2。*x*驱动程序不支持**SQLSetPos**与*操作*的 SQL_ADD，ODBC 3*.x*驱动程序管理器未映射**SQLSetPos**与*操作*的到 SQL_ADD **SQLBulkOperations**与*操作*SQL_ADD。 这是因为**SQLBulkOperations**不在状态 S7，哪些在 ODBC 2 中调用。*x*已在其中的唯一状态**SQLSetPos**无法调用。<br />-如果在应用程序调用**SQLBulkOperations**与*操作*的 ODBC 2 中的 SQL_ADD。*x*驱动程序之前调用**SQLFetchScroll**，ODBC 3*.x*驱动程序管理器将返回错误。|  
|**SQLExtendedFetch**|返回指定的行集。 只需说明，否则限制 ODBC 3 除外*.x*驱动程序管理器将传递到调用**SQLExtendedFetch**于驱动程序，而不考虑驱动程序版本。|  
|**SQLFetch**|返回下一步的行集。 以下是实现详细信息：<br /><br /> -如果应用程序调用**SQLFetch** ODBC 2 中。*x*驱动程序，ODBC 3*.x*驱动程序管理器将其映射到**SQLExtendedFetch**。 *FetchOrientation*参数**SQLExtendedFetch**设置为 SQL_FETCH_NEXT。 驱动程序管理器使用的 SQL_ATTR_ROW_STATUS_PTR 语句特性的缓存的值*RowStatusArray*自变量和 SQL_ATTR_ROWS_FETCHED_PTR 语句属性的缓存的值*RowCountPtr*自变量。<br />-An ODBC 3*.x*应用程序可以混合使用调用**SQLFetch**和**SQLFetchScroll** ODBC 2 中。*x*驱动程序因为 ODBC 3*.x*驱动程序管理器映射**SQLFetch**到**SQLExtendedFetch**应用程序时在 ODBC 2 中调用它。*x*驱动程序。<br />-如果检测到 ODBC 2。*x*驱动程序不支持**SQLExtendedFetch**，ODBC 3*.x*驱动程序管理器未映射**SQLFetch**或**SQLFetchScroll**到**SQLExtendedFetch**应用程序时在该驱动程序中调用它。 如果应用程序尝试将 SQL_ATTR_ROW_ARRAY_SIZE 设置为一个值大于 1，SQLSTATE HYC00 返回 （未实现的可选功能）。<br />-除了有关限制只需说明，否则，ODBC 3*.x*驱动程序管理器将传递到调用**SQLFetch**于驱动程序，而不考虑驱动程序版本。|  
|**SQLFetchScroll**|返回指定的行集。 以下是实现详细信息：<br /><br /> -如果应用程序调用**SQLFetchScroll** ODBC 2 中。*x*驱动程序，ODBC 3*.x*驱动程序管理器将其映射到**SQLExtendedFetch**。 它使用的 SQL_ATTR_ROW_STATUS_PTR 语句特性的缓存的值*RowStatusArray*自变量和 SQL_ATTR_ROWS_FETCHED_PTR 语句属性的缓存的值*RowCountPtr*自变量。 如果*FetchOrientation*中的参数**SQLFetchScroll**是 SQL_FETCH_BOOKMARK，它使用的 SQL_ATTR_FETCH_BOOKMARK_PTR 语句特性的缓存的值*FetchOffset*自变量并返回错误，如果*FetchOffset*参数**SQLFetchScroll**是不是 0。<br />-如果应用程序调用这 ODBC 3 中*.x*驱动程序，ODBC 3*.x*驱动程序管理器将传递到该驱动程序的调用。|  
|**SQLSetPos**|执行各种定位的操作。 ODBC 3*.x*驱动程序管理器将传递到调用**SQLSetPos**于驱动程序，而不考虑驱动程序版本。|  
|**SQLSetScrollOptions**|当驱动程序管理器映射**SQLSetScrollOptions**为应用程序使用 ODBC 3*.x*驱动程序不支持**SQLSetScrollOptions**，驱动程序管理器将设置 SQL_ROWSET_SIZE 语句选项，不 SQL_ATTR_ROW_ARRAY_SIZE 语句特性，为*RowsetSize*中的参数**SQLSetScrollOption**。 因此， **SQLSetScrollOptions**按调用提取多行时，应用程序不使用**SQLFetch**或**SQLFetchScroll**。 仅当通过调用提取多个行时，才可以使用它**SQLExtendedFetch**。|

