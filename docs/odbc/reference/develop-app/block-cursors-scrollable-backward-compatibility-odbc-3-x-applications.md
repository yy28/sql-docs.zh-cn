---
title: 块和适用于 ODBC 的可滚动游标兼容性 3.x |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- SQLExtendedFetch function [ODBC], block cursors
- cursors [ODBC], compatibility issues
- SQLFetchScroll function [ODBC], block cursors
ms.assetid: 82f6cf68-cfde-4417-9788-d6382ca14bf8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 670c81a8af1ec229a22ad9a8d52c8bab7164fdd1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>块状游标可滚动游标，对于 ODBC 3.x 应用程序的向后兼容性
同时存在**SQLFetchScroll**和**SQLExtendedFetch**首先清除拆分 ODBC 之间应用程序编程接口 (API)，这是组的函数中的表示应用程序调用和服务提供程序接口 (SPI)，这是函数的一套驱动程序实现。 此拆分需要平衡 ODBC 3 中的要求。*x*，它使用**SQLFetchScroll**、 要与标准保持一致，并且与 ODBC 2 兼容。*x*，它使用**SQLExtendedFetch**。  
  
 ODBC 3 *.x* api，该 API 的一套应用程序调用的函数、 包括**SQLFetchScroll**和相关语句属性。 ODBC 3 *.x* SPI，是一组函数的驱动程序实现，包括**SQLFetchScroll**， **SQLExtendedFetch**，以及相关语句属性。 因为 ODBC 不会准确地讲强制 API 和 SPI 之间的这种分割，所以有可能 ODBC 3 *.x*应用程序调用**SQLExtendedFetch**和相关语句属性。 但是，没有没有理由 ODBC 3 *.x*应用程序来执行此操作。 有关 Api 和 Spi 的详细信息，请参阅简介[ODBC 体系结构](../../../odbc/reference/odbc-architecture.md)。  
  
 有关如何信息 ODBC 3。*x*驱动程序管理器将调用映射到 ODBC 2。*x*和 ODBC 3。*x*驱动程序和哪些函数和语句属性 ODBC 3。*x*驱动程序应该实现块和可滚动游标，请参阅[驱动程序的用途](../../../odbc/reference/appendixes/what-the-driver-does.md)为了向后兼容的附录 g： 驱动程序准则中。  
  
 下表总结了哪些功能和语句特性 ODBC 3。*x*应用程序应使用块和可滚动的光标。 它还列出了 ODBC 2 之间的更改。*x*和 ODBC 3。*x*在此区域该 ODBC 3。*x*应用程序应注意的是与 ODBC 2 兼容。*x*驱动程序。  
  
|函数或<br /><br /> 语句属性|注释|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向该书签用于**SQLFetchScroll**。<br /><br /> 当应用程序设置此 ODBC 2 中。*x*驱动程序，它必须指向固定长度书签。|  
|SQL_ATTR_ROW_STATUS_PTR|指向行状态数组由填写**SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，和**SQLSetPos**。<br /><br /> 如果应用程序在 ODBC 2 中设置此操作。*x*驱动程序和调用**SQLBulkOperation**与*操作*SQL_ADD 之前调用的**SQLFetchScroll**， **SQLFetch**，或**SQLExtendedFetch**，SQLSTATE HY011 （不能设置属性现在） 返回。<br /><br /> 在应用程序调用**SQLFetch** ODBC 2 中。*x*驱动程序， **SQLFetch**映射到**SQLExtendedFetch**并因此此数组中返回值。|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向在其中缓冲区**SQLFetch**和**SQLFetchScroll**返回提取的行数。<br /><br /> 在应用程序调用**SQLFetch** ODBC 2 中。*x*驱动程序， **SQLFetch**映射到**SQLExtendedFetch**并因此在此缓冲区中返回一个值。|  
|SQL_ATTR_ROW_ARRAY_SIZE|设置行集大小。<br /><br /> 如果应用程序调用**SQLBulkOperations**与*操作*的 ODBC 2 中的 SQL_ADD。*x*驱动程序，SQL_ROWSET_SIZE 将用于调用不 SQL_ATTR_ROW_ARRAY_SIZE，因为调用映射到**SQLSetPos**与*操作*的 SQL_ADD，使用SQL_ROWSET_SIZE。<br /><br /> 调用**SQLSetPos**与*操作*的 SQL_ADD 或**SQLExtendedFetch** ODBC 2 中。*x*驱动程序使用 SQL_ROWSET_SIZE。<br /><br /> 调用**SQLFetch**或**SQLFetchScroll** ODBC 2 中。*x*驱动程序使用 SQL_ATTR_ROW_ARRAY_SIZE。|  
|**SQLBulkOperations**|执行插入和书签的操作。 当**SQLBulkOperations**与*操作*SQL_ADD 称为 ODBC 2 中。*x*驱动程序，它将映射到**SQLSetPos**与*操作*SQL_ADD。 以下是实现详细信息：<br /><br /> -当使用 ODBC 2。*x*驱动程序，应用程序必须使用仅与关联的隐式分配的 ARD *StatementHandle*; 它不能用于添加行，分配另一个 ARD，由于显式描述符操作属于不支持 ODBC 2。*x*驱动程序。 应用程序必须使用**SQLBindCol**不绑定到 ARD， **SQLSetDescField**或**SQLSetDescRec**。<br />-当调用 ODBC 3。*x*驱动程序，应用程序可以调用**SQLBulkOperations**与*操作*SQL_ADD 之前调用的**SQLFetch**或**SQLFetchScroll**。 调用 ODBC 2 时。*x*驱动程序，应用程序必须调用**SQLFetchScroll**之前调用**SQLBulkOperations**与 SQL_ADD 的操作。|  
|**SQLFetch**|返回下一步的行集。 以下是实现详细信息：<br /><br /> -如果应用程序调用**SQLFetch** ODBC 2 中。*x*驱动程序，它将映射到**SQLExtendedFetch**。<br />-如果应用程序调用**SQLFetch** ODBC 3 中。*x*驱动程序，它将返回具有 SQL_ATTR_ROW_ARRAY_SIZE 语句属性指定的行数。|  
|**SQLFetchScroll**|返回指定的行集。 以下是实现详细信息：<br /><br /> -如果应用程序调用**SQLFetchScroll** ODBC 2 中。*x*驱动程序，它将返回 SQLSTATE 01S01 （行中的错误） 之前每个错误都适用于单个行。 不过这只是因为 ODBC 3 *.x*驱动程序管理器映射到**SQLExtendedFetch**和**SQLExtendedFetch**返回此 SQLSTATE。 在应用程序调用**SQLFetchScroll** ODBC 3 中。*x*驱动程序，它绝不会返回 SQLSTATE 01S01 （行中的错误）。<br />-如果应用程序调用**SQLFetchScroll** ODBC 2 中。*x*驱动程序与*FetchOrientation*设置为 SQL_FETCH_BOOKMARK， *FetchOffset*参数必须设置为 0。 SQLSTATE HYC00 如果基于偏移量的书签提取，将尝试使用 ODBC 2，则返回 （未实现的可选功能）。*x*驱动程序。|  
  
> [!NOTE]  
>  ODBC 3。*x*应用程序不应使用**SQLExtendedFetch**或 SQL_ROWSET_SIZE 语句属性。 相反，它们应使用**SQLFetchScroll**和 SQL_ATTR_ROW_ARRAY_SIZE 语句属性。 ODBC 3。*x*应用程序不应使用**SQLSetPos**与*操作*的 SQL_ADD 但应使用**SQLBulkOperations**与*操作*SQL_ADD。
