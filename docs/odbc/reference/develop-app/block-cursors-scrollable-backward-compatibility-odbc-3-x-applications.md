---
title: ODBC 2.x 的块和可滚动游标兼容性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- SQLExtendedFetch function [ODBC], block cursors
- cursors [ODBC], compatibility issues
- SQLFetchScroll function [ODBC], block cursors
ms.assetid: 82f6cf68-cfde-4417-9788-d6382ca14bf8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c526eff6e19014c923f05ad91551a7d7c66f5294
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306338"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>ODBC 3.x 应用程序的块游标、可滚动游标和后向兼容性
**SQLFetchScroll**和**SQLExtendedFetch**的存在都表示应用程序编程接口（API）（它是应用程序调用的函数集）与服务提供程序接口（SPI）之间的 ODBC 中的第一个明确拆分，后者是驱动程序实现的函数集。 需要此拆分来*平衡 odbc 2.x*中的要求，该要求使用**SQLFetchScroll**，以符合标准并与使用**SQLExtendedFetch***的 odbc 2.x 兼容。*  
  
 *ODBC 2.X* API 是应用程序调用的函数集，包括**SQLFetchScroll**和相关语句属性。 *ODBC 2.X* SPI 是驱动程序实现的一组函数，包括**SQLFetchScroll**、 **SQLExtendedFetch**和相关的语句属性。 由于 ODBC 不会在 API 与 SPI 之间正式强制实现此拆分，因此，ODBC *1.x 应用程序*可以调用**SQLExtendedFetch**和相关的语句属性。 不过 *，ODBC 1.x*应用程序没有理由执行此操作。 有关 Api 和 SPIs 的详细信息，请参阅[ODBC 体系结构](../../../odbc/reference/odbc-architecture.md)简介。  
  
 有关 ODBC *1.X 驱动程序*管理器如何映射对 odbc 2.x 驱动程序和*odbc 2.x*驱动程序的调用，*以及 odbc 2.x* *驱动程序应*为块和可滚动游标实现哪些函数和语句属性的信息，请参阅附录 G：驱动程序指南中的[驱动程序功能](../../../odbc/reference/appendixes/what-the-driver-does.md)以了解向后兼容性。  
  
 下表总结*了 ODBC 2.x*应用程序应将哪些函数和语句特性用于块和可滚动游标。 它还列出了 ODBC 2.x*和 odbc* *2.x 在此区域中的更改*，odbc 3.x 应用程序应该知道*与 odbc 2.x* *驱动程序兼容*。  
  
|函数或<br /><br /> 语句特性|说明|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向要用于**SQLFetchScroll**的书签。<br /><br /> 当应用程序*在 ODBC 2.x*驱动程序中设置此项时，它必须指向固定长度的书签。|  
|SQL_ATTR_ROW_STATUS_PTR|指向由**SQLFetch**、 **SQLFetchScroll**、 **SQLBulkOperations**和**SQLSetPos**填充的行状态数组。<br /><br /> 如果应用程序*在 ODBC 2.x*驱动程序中设置此项，并在调用**SQLFetchScroll**、 **SQLFetch**或**SQLExtendedFetch**之前使用 SQL_ADD 的*操作*调用**SQLBulkOperation** ，则会返回 SQLSTATE HY011 （现在不能设置特性）。<br /><br /> 当应用程序*在 ODBC 2.x*驱动程序中调用**SQLFetch**时， **SQLFetch**将映射到**SQLExtendedFetch** ，因而返回此数组中的值。|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向缓冲区，其中**SQLFetch**和**SQLFetchScroll**返回提取的行数。<br /><br /> 当应用程序*在 ODBC 2.x*驱动程序中调用**SQLFetch**时， **SQLFetch**将映射到**SQLExtendedFetch** ，因此在此缓冲区中返回一个值。|  
|SQL_ATTR_ROW_ARRAY_SIZE|设置行集大小。<br /><br /> 如果应用程序*在 ODBC 2.x*驱动程序中使用 SQL_ADD 的*操作*调用**SQLBulkOperations** ，则 SQL_ROWSET_SIZE 将用于调用，而不是 SQL_ATTR_ROW_ARRAY_SIZE，因为调用会映射到使用 SQL_ADD*操作*的**SQLSetPos** ，这将使用 SQL_ROWSET_SIZE。<br /><br /> 在*ODBC 2.x*驱动程序中使用 SQL_ADD**或 SQLExtendedFetch**的*操作*调用**SQLSetPos**时使用 SQL_ROWSET_SIZE。<br /><br /> 在*ODBC 2.x*驱动程序中调用**SQLFetch**或**SQLFetchScroll**将使用 SQL_ATTR_ROW_ARRAY_SIZE。|  
|**SQLBulkOperations**|执行插入和书签操作。 当*在 ODBC 2.x*驱动程序中调用 SQL_ADD*操作*的**SQLBulkOperations**时，它将映射到具有 SQL_ADD*操作*的**SQLSetPos** 。 下面是实现的详细信息：<br /><br /> -*使用 ODBC 2.x 驱动程序时*，应用程序必须仅使用与*StatementHandle*关联的隐式分配的 ARD;由于 ODBC 2.x 驱动程序不支持显式描述符操作，因此它不能分配另一个 ARD 来添加*行。* 应用程序必须使用**SQLBindCol**绑定到 ARD，而不是**SQLSetDescField**或**SQLSetDescRec**。<br />-*调用 ODBC 1.x*驱动程序时，应用程序可以调用 SQL_ADD **SQLBulkOperations** ，然后调用*Operation* **SQLFetch**或**SQLFetchScroll**。 调用*ODBC 2.x*驱动程序时，应用程序必须先调用**SQLFetchScroll** ，然后才能调用具有 SQL_ADD 操作的**SQLBulkOperations** 。|  
|**SQLFetch**|返回下一个行集。 下面是实现的详细信息：<br /><br /> -当应用程序*在 ODBC 2.x*驱动程序中调用**SQLFetch**时，它将映射到**SQLExtendedFetch**。<br />-当应用程序*在 ODBC 1.x*驱动程序中调用**SQLFetch**时，它将返回使用 SQL_ATTR_ROW_ARRAY_SIZE 语句特性指定的行数。|  
|**SQLFetchScroll**|返回指定的行集。 下面是实现的详细信息：<br /><br /> -当应用程序*在 ODBC 2.x*驱动程序中调用**SQLFetchScroll**时，它将在应用于单个行的每个错误之前返回 SQLSTATE 01S01 （行中的错误）。 这只是*因为 ODBC 2.X*驱动程序管理器将此映射到**SQLExtendedFetch** ， **SQLExtendedFetch**返回此 SQLSTATE。 当应用程序*在 ODBC 1.x*驱动程序中调用**SQLFetchScroll**时，它绝不会返回 SQLSTATE 01S01 （行中的错误）。<br />-当应用程序*在 ODBC 2.x*驱动程序中调用**SQLFetchScroll**时，如果*FetchOrientation*设置为 SQL_FETCH_BOOKMARK，则*FetchOffset*参数必须设置为0。 如果尝试*使用 ODBC 2.x*驱动程序进行基于偏移量的书签提取，则返回 SQLSTATE HYC00 （未实现可选功能）。|  
  
> [!NOTE]  
>  ODBC *2.x*应用程序不应使用**SQLExtendedFetch**或 SQL_ROWSET_SIZE 语句特性。 相反，它们应使用**SQLFetchScroll**和 SQL_ATTR_ROW_ARRAY_SIZE 语句特性。 ODBC *2.x*应用程序不应将**SQLSetPos**与 SQL_ADD 的*操作*一起使用，但应将**SQLBulkOperations**与*操作*SQL_ADD 的操作一起使用。
