---
title: SQLFetchScroll（光标库） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetchScroll function [ODBC], Cursor Library
ms.assetid: 4417e57c-31dd-475e-8fe9-eab00a459c80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e5573b8afc49afec8b7afa4fc52590e7a6a9e2fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302048"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLFetchScroll**函数。 有关**SQLFetchScroll 的**一般信息，请参阅[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
 游标库通过在驱动程序中重复调用**SQLFetch**实现**SQLFetch。** 它将从驱动程序检索到的数据传输到应用程序提供的行集缓冲区。 它还将数据缓存在内存和磁盘文件中。 当应用程序请求新的行集时，游标库根据需要从驱动程序（如果以前未提取）或缓存（如果以前已提取）中检索它。 最后，游标库维护缓存数据的状态，并将此信息返回到行状态数组中的应用程序。  
  
 使用游标库时，对**SQLFetchScroll**的调用不能与**SQLFetch**或**SQL 扩展获取的**调用混合。  
  
 使用游标库时，ODBC 2 都支持对**SQLFetchScroll 的**调用。*x*和 ODBC 3。*x*驱动程序。  
  
## <a name="rowset-buffers"></a>行集缓冲区  
 在以下情况下，游标库优化了数据从驱动程序传输到应用程序提供的行集缓冲区：  
  
-   应用程序使用行绑定。  
  
-   应用程序声明为保存一行数据的结构中的字段之间没有未使用的字节。  
  
-   **SQLFetch**或**SQLFetchScroll**返回列的长度/指示器的字段遵循该列的缓冲区，并在下一列的缓冲区之前。 这些字段是可选的。  
  
 当应用程序请求新的行集时，游标库根据需要从其缓存和驱动程序检索数据。 如果新旧行集重叠，游标库可以通过重用行集缓冲区重叠部分的数据来优化其性能。 因此，除非新旧行集重叠，并且更改位于行集缓冲区的重叠部分，否则将丢失对行集缓冲区的未保存更改。 要保存更改，应用程序将提交定位的更新语句。  
  
 请注意，当应用程序调用**SQLFetchScroll**时，光标库始终使用缓存中的数据刷新行集缓冲区，其中*Fetch定向*参数设置为SQL_FETCH_RELATIVE，FetchOffset*FetchOffset*参数设置为 0。  
  
 游标库支持使用SQL_ATTR_ROW_ARRAY_SIZE*属性*调用**SQLSetStmtAttr，** 以在游标打开时更改行集大小。 下次调用**SQLFetchScroll**时，新的行集大小将生效。  
  
## <a name="result-set-membership"></a>结果集成员资格  
 游标库仅在应用程序请求时从驱动程序检索数据。 根据数据源和SQL_CONCURRENCY语句属性的设置，这会产生以下后果：  
  
-   游标库检索的数据可能与执行语句时可用的数据不同。 例如，在打开游标后，某些驱动程序可以检索插入在当前游标位置以外的点插入的行。  
  
-   结果集中的数据可能由游标库的数据源锁定，因此其他用户不可用。  
  
 游标库缓存一行数据后，无法检测对基础数据源中该行的更改（定位更新和在同一游标缓存上运行的删除除外）。 这是因为，对于**SQLFetchScroll 的**调用，游标库从不从数据源重新提取数据。 相反，它会从缓存中重新提取数据。  
  
## <a name="scrolling"></a>滚动  
 游标库支持**SQLFetchScroll**中的以下提取类型。  
  
|光标类型|提取类型|  
|-----------------|-----------------|  
|只进|SQL_FETCH_NEXT|  
|Static|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>错误  
 当调用**SQLFetchScroll**并返回**SQLFetch**的调用之一SQL_ERROR时，光标库将如下所示。 完成这些步骤后，光标库将继续处理。  
  
1.  调用**SQLGetDiagRec**从驱动程序获取错误信息，并将其作为诊断记录张贴在驱动程序管理器中。  
  
2.  将诊断记录中SQL_DIAG_ROW_NUMBER字段设置为适当的值。  
  
3.  将诊断记录中的SQL_DIAG_COLUMN_NUMBER字段设置为适当的值（如果适用）;否则，它将设置为 0。  
  
4.  将行状态数组中出错行的值设置为SQL_ROW_ERROR。  
  
 游标库在实现**SQLFetchScroll**时多次调用**SQLFetch**后，对**SQLFetch**的调用返回的任何错误或警告都将位于诊断记录中，并且可以通过调用**SQLGetDiagRec**来检索。 如果数据在提取时被截断，则截断的数据现在将驻留在游标库的缓存中。 后续对**SQLFetchScroll**的调用以滚动到具有截断数据的行将返回截断的数据，并且不会引发任何警告，因为数据是从光标库的缓存中获取的。 为了跟踪返回的数据长度，以便确定缓冲区中返回的数据是否已截断，应用程序应绑定长度/指示器缓冲区。  
  
## <a name="bookmark-operations"></a>书签操作  
 游标库支持使用SQL_FETCH_BOOKMARK*的取取方向*调用**SQLFetchScroll。** 它还支持在 *"提取偏移"* 参数中指定可在书签操作中使用的偏移量。 这是光标库支持的唯一书签操作。 游标库不支持调用**SQLBulk 操作**。  
  
 如果应用程序已设置SQL_ATTR_USE_BOOKMARKS语句属性并绑定到书签列，则游标库将生成一个固定长度的书签并将其返回到应用程序。 游标库创建和维护它使用的书签;它不使用在数据源中维护的书签。 当调用**SQLFetchScroll**来检索已经从数据源获取的数据块时，它会从游标库缓存中检索数据。 因此，在调用**SQLFetchScroll**时使用的书签（带有SQL_FETCH_BOOKMARK*的取取方向*必须由游标库创建和维护。  
  
## <a name="interaction-with-other-functions"></a>与其他函数的交互  
 应用程序必须调用**SQLFetch**或**SQLFetchScroll，** 然后才能准备或执行任何定位的更新或删除语句。
