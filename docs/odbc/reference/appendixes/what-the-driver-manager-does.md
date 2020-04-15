---
title: 驱动程序管理器的作用 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07ab0784e6f6ad4487a02a179a5fa3be2617c930
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306558"
---
# <a name="what-the-driver-manager-does"></a>驱动程序管理器的用途
下表总结了 ODBC *3.x*驱动程序管理器如何将调用映射到 ODBC *2.x*和 ODBC *3.x*驱动程序。  
  
|功能或<br /><br /> 语句属性|注释|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向书签以与**SQLFetchScroll**一起使用。 以下是实现详细信息：<br /><br /> - 当应用程序在 ODBC *2.x*驱动程序中设置此参数时，ODBC *3.x*驱动程序管理器会缓存它。 它引用指针并将值传递给**SQL 扩展提取***的 Fetch 偏移*参数中的 ODBC *2.x*驱动程序，而稍后应用程序调用**SQLFetchScroll。**<br />- 当应用程序在 ODBC *3.x*驱动程序中设置此驱动程序时，ODBC *3.x*驱动程序管理器将呼叫传递给驱动程序。|  
|SQL_ATTR_ROW_STATUS_PTR|指向由**SQLFetch、SQLFetchScroll、SQLBulk****操作**和**SQLSetPos**填充的行状态数组。 **SQLFetch** 以下是实现详细信息：<br /><br /> - 当应用程序在 ODBC *2.x*驱动程序中设置此值时，ODBC *3.x*驱动程序管理器缓存其值。 当调用**SQLFetchScroll 或** **SQLFetch**时，它将此值传递给**SQLAa 的 SQLAa** *参数*中的 ODBC *2.x*驱动程序。<br />- 当应用程序在 ODBC *3.x*驱动程序中设置此驱动程序时，ODBC *3.x*驱动程序管理器将呼叫传递给驱动程序。<br />- 在状态 S6 中，如果应用程序设置SQL_ATTR_ROW_STATUS_PTR，然后调用**SQLBulk 操作**（操作SQL_ADD）或**SQLSetPos，** 而无需首先调用**SQLFetch**或**SQLFetchScroll，** 则返回 SQLSTATE HY011（现在无法设置属性）。 *Operation*|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向**SQLFetch**和**SQLFetchScroll**返回提取的行数的缓冲区。 以下是实现详细信息：<br /><br /> - 当应用程序在 ODBC *2.x*驱动程序中设置此值时，ODBC *3.x*驱动程序管理器缓存其值。 当应用程序调用**SQLFetch**或**SQLFetchScroll**时，它将此值传递给**SQL 扩展提取**的*RowCountPtr*参数中的 ODBC *2.x*驱动程序。<br />- 当应用程序在 ODBC *3.x*驱动程序中设置此驱动程序时，ODBC *3.x*驱动程序管理器将呼叫传递给驱动程序。|  
|SQL_ATTR_ROW_ARRAY_SIZE|设置行集大小。 以下是实现详细信息：<br /><br /> - 当应用程序在 ODBC *2.x*驱动程序中设置此驱动程序时，ODBC *3.x*驱动程序管理器将其映射到SQL_ROWSET_SIZE语句属性。<br />- 当应用程序在 ODBC *3.x*驱动程序中设置此驱动程序时，ODBC *3.x*驱动程序管理器将呼叫传递给驱动程序。<br />- 当使用 ODBC *3.x*驱动程序的应用程序调用**SQLSetScrollOptions**时，如果基础驱动程序不支持**SQLSetScrollOptions，** 则SQL_ROWSET_SIZE设置为*RowsetSize*参数中的值。|  
|SQL_ROWSET_SIZE|设置**SQL 扩展提取**在 ODBC *2.x*应用程序调用**SQL 扩展时**使用的行集大小。 以下是实现详细信息：<br /><br /> - 当应用程序设置此设置时，ODBC *3.x*驱动程序管理器将呼叫传递给驱动程序，而不考虑驱动程序版本。<br />- 当使用 ODBC *2.x*驱动程序的应用程序调用**SQLSetScrollOptions**时，SQL_ROWSET_SIZE设置为**RowsetSize**参数中的值。|  
|**SQLBulk 操作**|执行插入操作，或通过书签操作更新、删除或提取。 以下是实现详细信息：<br /><br /> - 当应用程序在 ODBC *2.x*驱动程序中调用**具有**SQL_ADD*操作时*，ODBC *3.x*驱动程序管理器将其映射到具有SQL_ADD*操作*的**SQLSetPos。**<br />- 当使用不支持**SQLSetPos**的 ODBC *2.x*驱动程序*Operation*操作SQL_ADD时，ODBC *3.x*驱动程序管理器不会将**SQLSetPos**具有SQL_ADD*操作*映射到具有SQL_ADD*操作*的**SQLBulk 操作**。 这是因为**SQLBulk 操作**不能在状态 S7 中调用，在 ODBC *2.x*中，这是可以调用**SQLSetPos**的唯一状态。<br />- 如果应用程序在调用**SQLFetchScroll**之前在 ODBC *2.x*驱动程序中调用**SQLBulk 操作**，操作SQL_ADD，则 ODBC *3.x*驱动程序管理器将返回错误。 *Operation*|  
|**SQL 扩展获取**|返回指定的行集。 除了刚才注意到的限制之外，ODBC *3.x*驱动程序管理器将呼叫传递给**SQLExtendedFetch**的驱动程序，而不管驱动程序版本如何。|  
|**SQLFetch**|返回下一个行集。 以下是实现详细信息：<br /><br /> - 当应用程序在 ODBC *2.x*驱动程序中调用**SQLFetch**时，ODBC *3.x*驱动程序管理器将其映射到**SQL 扩展获取**。 **SQL 扩展获取**的*提取方向*参数设置为SQL_FETCH_NEXT。 驱动程序管理器使用*rowStatusArray*参数的SQL_ATTR_ROW_STATUS_PTR语句属性的缓存值和*RowCountPtr*参数SQL_ATTR_ROWS_FETCHED_PTR语句属性的缓存值。<br />- ODBC *3.x*应用程序可以在 ODBC *2.x*驱动程序中混合对**SQLFetch**和**SQLFetchScroll**的调用，因为当应用程序在 ODBC *2.x*驱动程序中调用 SQLFetch 时，ODBC *3.x*驱动程序管理器将**SQLFetch**映射到**SQLExtendedFetch。**<br />- 如果 ODBC *2.x*驱动程序不支持**SQLExtendedFetch，** 则当应用程序在该驱动程序中调用 SQL 提取时，ODBC *3.x*驱动程序管理器不会将**SQLFetch**或**SQLFetchScroll**映射到**SQL 扩展获取**。 如果应用程序尝试将SQL_ATTR_ROW_ARRAY_SIZE设置为大于 1 的值，则返回 SQLSTATE HYC00（未实现可选功能）。<br />- 除了刚才注意到的限制之外，ODBC *3.x*驱动程序管理器将呼叫传递给**SQLFetch**的驱动程序，而不管驱动程序版本如何。|  
|**SQLFetchScroll**|返回指定的行集。 以下是实现详细信息：<br /><br /> - 当应用程序在 ODBC *2.x*驱动程序中调用**SQLFetchScroll**时，ODBC *3.x*驱动程序管理器将其映射到**SQL 扩展获取**。 它使用*rowStatusArray*参数的 SQL_ATTR_ROW_STATUS_PTR 语句属性的缓存值和*RowCountPtr*参数的SQL_ATTR_ROWS_FETCHED_PTR语句属性的缓存值。 如果*SQLFetchScroll* **SQLFetchScroll**中的 Fetch 方向参数SQL_FETCH_BOOKMARK，它将使用*fetchOffset*参数的SQL_ATTR_FETCH_BOOKMARK_PTR语句属性的缓存值，如果**SQLFetchScroll**的*FetchOffset*参数不是 0，则返回错误。<br />- 当应用程序在 ODBC *3.x*驱动程序中调用此呼叫时，ODBC *3.x*驱动程序管理器将呼叫传递给驱动程序。|  
|**SQLSetPos**|执行各种定位操作。 无论驱动程序版本如何，ODBC *3.x*驱动程序管理器都会将对**SQLSetPos**的调用传递给驱动程序。|  
|**SQLSetScroll 选项**|当驱动程序管理器映射**SQLSetScrollOption 的应用程序 SQLSetScrollOption**时，使用不支持**SQLSetScrollOption**的 ODBC *3.x*驱动程序时，驱动程序管理器将SQL_ROWSET_SIZE语句选项（而不是SQL_ATTR_ROW_ARRAY_SIZE语句属性）设置为**SQLSetScrollOption**中的*RowsetSize*参数。 因此，当调用**SQLFetch**或**SQLFetchScroll**获取多行时，应用程序无法使用**SQLSetScrollOptions。** 它只能在调用**SQLExtendedFetch**获取多行时使用。|
