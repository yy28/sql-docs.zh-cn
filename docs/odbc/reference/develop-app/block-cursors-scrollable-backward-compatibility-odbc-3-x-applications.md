---
title: 块和用于 ODBC 的可滚动游标兼容性 3.x |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49a7a1af0f4b487baddfffa3e4f14d2a148b7a1d
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794042"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>ODBC 3.x 应用程序的块游标、可滚动游标和后向兼容性
这两者的存在**SQLFetchScroll**并**SQLExtendedFetch**表示首先清除拆分 ODBC 之间应用程序编程接口 (API)，这是组的函数中服务提供程序接口 (SPI)，这是组的函数和应用程序调用，该驱动程序实现。 此拆分所需平衡 ODBC 中的要求*3.x*，使用**SQLFetchScroll**，以与标准保持一致，并与 ODBC 兼容*2.x*，使用**SQLExtendedFetch**。  
  
 ODBC *3.x* API，这是组函数的应用程序调用，包括**SQLFetchScroll**和相关的语句属性。 ODBC *3.x* SPI，这是一组函数的驱动程序实现，包括**SQLFetchScroll**， **SQLExtendedFetch**，和相关的语句属性。 由于 ODBC 不正式实施之间的 API 和 SPI 的划分，所以有可能适用于 ODBC *3.x*应用程序可以调用**SQLExtendedFetch**和相关的语句属性。 但是，没有适用于 ODBC 理由*3.x*应用程序来执行此操作。 有关 Api 和 Spi 的详细信息，请参阅简介[ODBC 体系结构](../../../odbc/reference/odbc-architecture.md)。  
  
 有关如何信息 ODBC *3.x*驱动程序管理器将调用映射到 ODBC *2.x*和 ODBC *3.x*驱动程序和函数和语句属性 ODBC *3.x*驱动程序应实现块和可滚动游标，请参阅[驱动程序的用途](../../../odbc/reference/appendixes/what-the-driver-does.md)中附录 g:为了向后兼容的驱动程序指南。  
  
 下表总结了哪些功能和语句属性 ODBC *3.x*应用程序应使用块和可滚动的光标。 它还列出了 ODBC 之间的更改*2.x*和 ODBC *3.x*此区域中该 ODBC *3.x*应用程序应注意的是与 ODBC 兼容*2.x*驱动程序。  
  
|函数或<br /><br /> 语句属性|注释|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向要用于该书签**SQLFetchScroll**。<br /><br /> 当应用程序设置此在 ODBC *2.x*驱动程序，这必须指向定长书签。|  
|SQL_ATTR_ROW_STATUS_PTR|指向行状态数组填充**SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，以及**SQLSetPos**。<br /><br /> 如果在 ODBC 中的应用程序设置这*2.x*驱动程序并调用**SQLBulkOperation**与*操作*的之前调用 SQL_ADD **SQLFetchScroll**， **SQLFetch**，或**SQLExtendedFetch**，SQLSTATE HY011 （属性不能立即设置） 返回。<br /><br /> 当应用程序调用**SQLFetch**在 ODBC *2.x*驱动程序**SQLFetch**映射到**SQLExtendedFetch**并因此返回此数组中的值。|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向的缓冲区**SQLFetch**并**SQLFetchScroll**返回提取的行数。<br /><br /> 当应用程序调用**SQLFetch**在 ODBC *2.x*驱动程序**SQLFetch**映射到**SQLExtendedFetch**并因此返回在此缓冲区中的值。|  
|SQL_ATTR_ROW_ARRAY_SIZE|设置行集大小。<br /><br /> 如果应用程序调用**SQLBulkOperations**与*操作*SQL_ADD 在 ODBC 中的*2.x* SQL_ROWSET_SIZE 的驱动程序，将用于调用不 SQL_ATTR_ROW_ARRAY_调整大小，因为调用映射到**SQLSetPos**与*操作*SQL_ADD，使用 SQL_ROWSET_SIZE。<br /><br /> 调用**SQLSetPos**与*操作*的 SQL_ADD 或**SQLExtendedFetch** ODBC 中*2.x*驱动程序将使用 SQL_ROWSET_SIZE。<br /><br /> 调用**SQLFetch**或**SQLFetchScroll** ODBC 中*2.x*驱动程序使用 SQL_ATTR_ROW_ARRAY_SIZE。|  
|**SQLBulkOperations**|执行 insert 和书签操作。 当**SQLBulkOperations**与*操作*SQL_ADD 的在 ODBC 中调用*2.x*驱动程序，它将映射到**SQLSetPos**与*操作*SQL_ADD。 以下是实现详细信息：<br /><br /> -当使用 ODBC *2.x*驱动程序，应用程序必须使用仅与关联的隐式分配的 ARD *StatementHandle*; 它不能分配另一个 ARD 添加行，因为显式描述符操作不支持 ODBC *2.x*驱动程序。 应用程序必须使用**SQLBindCol**将不绑定到 ARD **SQLSetDescField**或**SQLSetDescRec**。<br />-当调用 ODBC *3.x*驱动程序，应用程序可以调用**SQLBulkOperations**与*操作*的之前调用 SQL_ADD **SQLFetch**或**SQLFetchScroll**。 调用 ODBC 时*2.x*驱动程序，应用程序必须调用**SQLFetchScroll**之前调用**SQLBulkOperations** SQL_ADD 操作使用。|  
|**SQLFetch**|返回下一步的行集。 以下是实现详细信息：<br /><br /> -当应用程序调用**SQLFetch**在 ODBC *2.x*驱动程序，它将映射到**SQLExtendedFetch**。<br />-当应用程序调用**SQLFetch**在 ODBC *3.x*驱动程序，它将返回使用 SQL_ATTR_ROW_ARRAY_SIZE 语句属性指定的行数。|  
|**SQLFetchScroll**|返回指定行集。 以下是实现详细信息：<br /><br /> -当应用程序调用**SQLFetchScroll**在 ODBC *2.x*驱动程序，它将返回 SQLSTATE 01S01 （行中的错误） 之前应用于单个行的每个错误。 这是仅因为 ODBC *3.x*驱动程序管理器可以将其映射到**SQLExtendedFetch**并**SQLExtendedFetch**返回此的 SQLSTATE。 当应用程序调用**SQLFetchScroll**在 ODBC *3.x*驱动程序，它永远不会返回 SQLSTATE 01S01 （行中的错误）。<br />-当应用程序调用**SQLFetchScroll**在 ODBC *2.x*使用的驱动程序*FetchOrientation*设置为 SQL_FETCH_BOOKMARK， *FetchOffset*参数必须设置为 0。 SQLSTATE HYC00 如果偏移量基于书签提取，将尝试使用 ODBC，则返回 （未实现的可选功能） *2.x*驱动程序。|  
  
> [!NOTE]  
>  ODBC *3.x*应用程序不应使用**SQLExtendedFetch**或 SQL_ROWSET_SIZE 语句属性。 相反，它们应使用**SQLFetchScroll**和 SQL_ATTR_ROW_ARRAY_SIZE 语句属性。 ODBC *3.x*应用程序不应使用**SQLSetPos**与*操作*SQL_ADD 的但应使用**SQLBulkOperations**与*操作*SQL_ADD。
