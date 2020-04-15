---
title: ODBC 3.x 的块和可滚动光标兼容性 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306338"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>ODBC 3.x 应用程序的块游标、可滚动游标和后向兼容性
**SQLFetchScroll**和**SQLExtendedFetch**的存在代表了在 ODBC 中，应用程序编程接口 （API） 和服务提供者接口 （SPI） 之间的第一个明确拆分，这是驱动程序实现的函数集。 这种拆分是需要平衡使用**SQLFetchScroll**的 ODBC *3.x*中的需求，以便与标准保持一致，并与使用**SQLDbFetch**的 ODBC *2.x*兼容。  
  
 ODBC *3.x* API 是应用程序调用的功能集，包括**SQLFetchScroll**和相关语句属性。 ODBC *3.x* SPI 是驱动程序实现的函数集，包括**SQLFetchScroll、SQL****扩展获取**和相关语句属性。 由于 ODBC 未正式强制 API 和 SPI 之间的此拆分，因此 ODBC *3.x*应用程序可以调用**SQLExtendedFetch**和相关语句属性。 但是，ODBC *3.x*应用程序没有理由这样做。 有关 API 和 API 的详细信息，请参阅[ODBC 体系结构](../../../odbc/reference/odbc-architecture.md)的简介。  
  
 有关 ODBC *3.x*驱动程序管理器如何映射对 ODBC *2.x*和 ODBC *3.x*驱动程序的调用的信息，以及 ODBC *3.x*驱动程序应实现哪些功能和语句，以便块和可滚动游标，请参阅驱动程序在附录 G[中的作用](../../../odbc/reference/appendixes/what-the-driver-does.md)：向后兼容性的驱动程序指南。  
  
 下表总结了 ODBC *3.x*应用程序应使用块和可滚动游标的功能和语句属性。 它还列出了 ODBC *2.x*和 ODBC *3.x*在这一领域的变化，ODBC *3.x*应用程序应了解与 ODBC *2.x*驱动程序兼容。  
  
|功能或<br /><br /> 语句属性|注释|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向书签以与**SQLFetchScroll**一起使用。<br /><br /> 当应用程序在 ODBC *2.x*驱动程序中设置此设置时，这必须指向固定长度的书签。|  
|SQL_ATTR_ROW_STATUS_PTR|指向由**SQLFetch、SQLFetchScroll、SQLBulk****操作**和**SQLSetPos**填充的行状态数组。 **SQLFetch**<br /><br /> 如果应用程序在 ODBC *2.x*驱动程序中设置此内容，并在调用**SQLFetchScroll、SQLFetch**或**SQLFetch****SQL 扩展获取**之前调用**SQLBulk** SQL_ADD*操作*，则返回 SQLSTATE HY011（现在无法设置属性）。<br /><br /> 当应用程序在 ODBC *2.x*驱动程序中调用**SQLFetch**时 **，SQLFetch**将映射到**SQLExtendedFetch，** 因此返回此数组中的值。|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向**SQLFetch**和**SQLFetchScroll**返回提取的行数的缓冲区。<br /><br /> 当应用程序在 ODBC *2.x*驱动程序中调用**SQLFetch**时 **，SQLFetch**将映射到**SQLExtendedFetch，** 因此在此缓冲区中返回一个值。|  
|SQL_ATTR_ROW_ARRAY_SIZE|设置行集大小。<br /><br /> 如果应用程序在 ODBC *2.x*驱动程序中使用 SQL_ADD*操作*调用**SQLBulk 操作**，则SQL_ROWSET_SIZE将用于调用，而不是SQL_ATTR_ROW_ARRAY_SIZE，因为调用映射到**SQLSetPos，** 操作SQL_ADD使用SQL_ROWSET_SIZE。 *Operation*<br /><br /> 在 ODBC *2.x*驱动程序中使用 SQL_ADD或**SQL 扩展提取***的操作*调用**SQLSetPos**使用SQL_ROWSET_SIZE。<br /><br /> 在 ODBC *2.x*驱动程序中调用**SQLFetch**或**SQLFetchScroll**使用SQL_ATTR_ROW_ARRAY_SIZE。|  
|**SQLBulk 操作**|执行插入和书签操作。 在 ODBC *2.x*驱动程序中调用具有SQL_ADD*操作*的**SQLBulk 操作**时，它将映射到具有SQL_ADD*操作*的**SQLSetPos。** 以下是实现详细信息：<br /><br /> - 使用 ODBC *2.x*驱动程序时，应用程序必须仅使用与*语句句柄*关联的隐式分配的 ARD。它不能为添加行分配另一个 ARD，因为 ODBC *2.x*驱动程序不支持显式描述符操作。 应用程序必须使用**SQLBindCol**绑定到 ARD，而不是**SQLSetDescField**或**SQLSetDescRec**。<br />- 调用 ODBC *3.x*驱动程序时，应用程序可以在调用**SQLFetch**或**SQLFetchScroll**之前调用**SQLBulk** *操作*，操作SQL_ADD。 调用 ODBC *2.x*驱动程序时，应用程序必须在调用**SQLBulk 操作**SQL_ADD之前调用**SQLFetchScroll。**|  
|**SQLFetch**|返回下一个行集。 以下是实现详细信息：<br /><br /> - 当应用程序在 ODBC *2.x*驱动程序中调用**SQLFetch**时，它将映射到**SQL 扩展获取**。<br />- 当应用程序在 ODBC *3.x*驱动程序中调用**SQLFetch**时，它将返回使用SQL_ATTR_ROW_ARRAY_SIZE语句属性指定的行数。|  
|**SQLFetchScroll**|返回指定的行集。 以下是实现详细信息：<br /><br /> - 当应用程序在 ODBC *2.x*驱动程序中调用**SQLFetchScroll**时，它将在应用于单个行的每个错误之前返回 SQLSTATE 01S01（行中的错误）。 它之所以这样做，只是因为 ODBC *3.x*驱动程序管理器将其映射到**SQL 扩展获取****，SQL 扩展获取**返回此 SQLSTATE。 当应用程序在 ODBC *3.x*驱动程序中调用**SQLFetchScroll**时，它永远不会返回 SQLSTATE 01S01（行中的错误）。<br />- 当应用程序在 ODBC *2.x*驱动程序中调用**SQLFetchScroll，** 其中*Fetch方向*设置为SQL_FETCH_BOOKMARK时，必须将*FetchOffset 参数*设置为 0。 如果尝试使用 ODBC *2.x*驱动程序获取基于偏移的书签，则返回 SQLSTATE HYC00（未实现可选功能）。|  
  
> [!NOTE]  
>  ODBC *3.x*应用程序不应使用**SQLExtendedFetch**或SQL_ROWSET_SIZE语句属性。 相反，他们应该使用**SQLFetchScroll**和SQL_ATTR_ROW_ARRAY_SIZE语句属性。 ODBC *3.x*应用程序不应将**SQLSetPos**与SQL_ADD*操作*一起使用，而应将**SQLBulk 操作**与SQL_ADD操作一起*使用*。
