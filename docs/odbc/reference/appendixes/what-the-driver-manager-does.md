---
title: 驱动程序管理器会 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], backward compatibility
- compatibility [ODBC], driver manager
- ODBC driver manager [ODBC]
- backward compatibility [ODBC], driver manager
ms.assetid: 57f65c38-d9ee-46c8-9051-128224a582c6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f29a40db8b35b5915de1889996e7953b1a8ad3f8
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794085"
---
# <a name="what-the-driver-manager-does"></a>驱动程序管理器的用途
下表总结了如何 ODBC *3.x*驱动程序管理器将调用映射到 ODBC *2.x*和 ODBC *3.x*驱动程序。  
  
|函数或<br /><br /> 语句属性|注释|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向要用于该书签**SQLFetchScroll**。 以下是实现详细信息：<br /><br /> 应用程序-在 ODBC 中设置此*2.x*驱动程序，ODBC *3.x*驱动程序管理器对其进行缓存。 它取消引用指针并将值传递到 ODBC *2.x*中的驱动程序*FetchOffset*自变量**SQLExtendedFetch**时**SQLFetchScroll**应用程序更高版本调用。<br />应用程序-在 ODBC 中设置此*3.x*驱动程序，ODBC *3.x*驱动程序管理器将传递给驱动程序的调用。|  
|SQL_ATTR_ROW_STATUS_PTR|指向行状态数组填充**SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，以及**SQLSetPos**。 以下是实现详细信息：<br /><br /> 应用程序-在 ODBC 中设置此*2.x*驱动程序，ODBC *3.x*驱动程序管理器缓存其值。 它将此值传递到 ODBC *2.x*中的驱动程序*RowStatusArray*自变量**SQLExtendedFetch**时**SQLFetchScroll**或**SQLFetch**调用。<br />应用程序-在 ODBC 中设置此*3.x*驱动程序，ODBC *3.x*驱动程序管理器将传递给驱动程序的调用。<br />-在状态 S6，如果应用程序将 SQL_ATTR_ROW_STATUS_PTR，然后调用**SQLBulkOperations** (使用*操作*SQL_ADD 的) 或**SQLSetPos**没有首先调用**SQLFetch**或**SQLFetchScroll**，SQLSTATE HY011 （属性不能立即设置） 返回。|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向的缓冲区**SQLFetch**并**SQLFetchScroll**返回提取的行数。 以下是实现详细信息：<br /><br /> 应用程序-在 ODBC 中设置此*2.x*驱动程序，ODBC *3.x*驱动程序管理器缓存其值。 它将此值传递到 ODBC *2.x*中的驱动程序*RowCountPtr*自变量**SQLExtendedFetch**时**SQLFetch**或**SQLFetchScroll**应用程序调用。<br />应用程序-在 ODBC 中设置此*3.x*驱动程序，ODBC *3.x*驱动程序管理器将传递给驱动程序的调用。|  
|SQL_ATTR_ROW_ARRAY_SIZE|设置行集大小。 以下是实现详细信息：<br /><br /> 应用程序-在 ODBC 中设置此*2.x*驱动程序，ODBC *3.x*驱动程序管理器将其映射到 SQL_ROWSET_SIZE 语句属性。<br />应用程序-在 ODBC 中设置此*3.x*驱动程序，ODBC *3.x*驱动程序管理器将传递给驱动程序的调用。<br />-当应用程序使用 ODBC *3.x*驱动程序调用**SQLSetScrollOptions**，SQL_ROWSET_SIZE 设置中的值为*RowsetSize*参数如果基础驱动程序不支持**SQLSetScrollOptions**。|  
|SQL_ROWSET_SIZE|设置使用的行集大小**SQLExtendedFetch**时**SQLExtendedFetch** ODBC 调用*2.x*应用程序。 以下是实现详细信息：<br /><br /> -应用程序当设置此操作，ODBC *3.x*驱动程序管理器将传递给驱动程序，无论何种驱动程序版本的调用。<br />-当应用程序使用 ODBC *2.x*驱动程序调用**SQLSetScrollOptions**，SQL_ROWSET_SIZE 设置中的值为**RowsetSize**参数。|  
|**SQLBulkOperations**|执行插入操作或更新，删除或通过书签操作的提取。 以下是实现详细信息：<br /><br /> -当应用程序调用**SQLBulkOperations**与*操作*SQL_ADD 在 ODBC 中的*2.x*驱动程序，ODBC *3.x*驱动程序管理器将映射到**SQLSetPos**与*操作*SQL_ADD。<br />-当使用 ODBC *2.x*不支持的驱动程序**SQLSetPos**与*操作*的 SQL_ADD，ODBC *3.x*驱动程序未映射管理器**SQLSetPos**与*操作*的到 SQL_ADD **SQLBulkOperations**与*操作*的 SQL添加 （_A)。 这是因为**SQLBulkOperations**不能处于状态 S7，哪些在 ODBC 调用*2.x*已在其中的唯一状态**SQLSetPos**无法调用。<br />-如果应用程序调用**SQLBulkOperations**与*操作*SQL_ADD 在 ODBC 中的*2.x*驱动程序之前调用**SQLFetchScroll**，ODBC *3.x*驱动程序管理器将返回错误。|  
|**SQLExtendedFetch**|返回指定行集。 但只需说明，否则限制 ODBC *3.x*驱动程序管理器将传递到调用**SQLExtendedFetch**向驱动程序，无论何种驱动程序版本。|  
|**SQLFetch**|返回下一步的行集。 以下是实现详细信息：<br /><br /> -当应用程序调用**SQLFetch**在 ODBC *2.x*驱动程序，ODBC *3.x*驱动程序管理器将映射到**SQLExtendedFetch**。 *FetchOrientation*的参数**SQLExtendedFetch**设置为 SQL_FETCH_NEXT。 驱动程序管理器使用缓存的 SQL_ATTR_ROW_STATUS_PTR 语句属性的值*RowStatusArray*自变量和 SQL_ATTR_ROWS_FETCHED_PTR 语句属性的缓存的值*RowCountPtr*参数。<br />-ODBC *3.x*应用程序可以混合使用调用**SQLFetch**并**SQLFetchScroll** ODBC 中*2.x*驱动程序由于 ODBC *3.x*驱动程序管理器映射**SQLFetch**到**SQLExtendedFetch**应用程序时在 ODBC 中调用它*2.x*驱动程序。<br />-如果检测到 ODBC *2.x*驱动程序不支持**SQLExtendedFetch**，ODBC *3.x*驱动程序管理器不会映射**SQLFetch**或**SQLFetchScroll**到**SQLExtendedFetch**应用程序时在该驱动程序中调用它。 如果应用程序尝试将 SQL_ATTR_ROW_ARRAY_SIZE 设置为值大于 1，SQLSTATE HYC00 返回 （未实现的可选功能）。<br />-除对于只是所述的限制，ODBC *3.x*驱动程序管理器将传递到调用**SQLFetch**向驱动程序，无论何种驱动程序版本。|  
|**SQLFetchScroll**|返回指定行集。 以下是实现详细信息：<br /><br /> -当应用程序调用**SQLFetchScroll**在 ODBC *2.x*驱动程序，ODBC *3.x*驱动程序管理器将映射到**SQLExtendedFetch**。 它使用缓存的 SQL_ATTR_ROW_STATUS_PTR 语句属性的值*RowStatusArray*自变量和 SQL_ATTR_ROWS_FETCHED_PTR 语句属性的缓存的值*RowCountPtr*自变量。 如果*FetchOrientation*中的参数**SQLFetchScroll**是 SQL_FETCH_BOOKMARK，它使用 SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性的缓存的值*FetchOffset*参数并返回错误，如果*FetchOffset*自变量**SQLFetchScroll**是不是 0。<br />-当应用程序调用这在 ODBC *3.x*驱动程序，ODBC *3.x*驱动程序管理器将传递给驱动程序的调用。|  
|**SQLSetPos**|执行各种定位的操作。 ODBC *3.x*驱动程序管理器将传递到调用**SQLSetPos**向驱动程序，无论何种驱动程序版本。|  
|**SQLSetScrollOptions**|当驱动程序管理器映射**SQLSetScrollOptions**应用程序使用 ODBC *3.x*不支持的驱动程序**SQLSetScrollOptions**，驱动程序管理器将设置 SQL_ROWSET_SIZE 语句选项，不将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性，为*RowsetSize*中的参数**SQLSetScrollOption**。 因此， **SQLSetScrollOptions**由在调用提取多行时，应用程序不能使用**SQLFetch**或**SQLFetchScroll**。 仅当通过调用提取多行时，可以使用它**SQLExtendedFetch**。|
