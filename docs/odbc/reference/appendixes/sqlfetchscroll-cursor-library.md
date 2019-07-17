---
title: SQLFetchScroll （游标库） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16e7e4d133fdfafd7a005c19b0a2943b2ea9ef6d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086456"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLFetchScroll**游标库中的函数。 有关常规信息**SQLFetchScroll**，请参阅[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
 游标库实现**SQLFetchScroll**通过反复调用**SQLFetch**驱动程序中。 它将它从驱动程序将检索到应用程序提供的行集缓冲区数据传输。 它还将缓存内存和磁盘文件中的数据。 当应用程序请求的新行集时，该游标库检索它根据需要从驱动程序 （如果它尚未以前提取） 或缓存 （如果它具有已事先提取）。 最后，该游标库保留缓存数据的状态，并将此信息返回给行状态数组中的应用程序。  
  
 当使用游标库时，调用**SQLFetchScroll**不能在其中调用**SQLFetch**或**SQLExtendedFetch**。  
  
 当使用游标库时，调用**SQLFetchScroll**都支持 ODBC 2。*x*以及 ODBC 3。*x*驱动程序。  
  
## <a name="rowset-buffers"></a>行集的缓冲区  
 游标库优化了数据驱动程序传输到应用程序如果提供的行集缓冲区：  
  
-   应用程序使用按行绑定。  
  
-   中的应用程序声明来保存数据的行的结构字段之间有任何未使用的字节。  
  
-   在其中的字段**SQLFetch**或**SQLFetchScroll**返回的列遵循为该列的缓冲区与之前的下一列的缓冲区长度/指示器。 这些字段是可选的。  
  
 当应用程序请求的新行集时，游标库检索数据，从其缓存和根据需要的驱动程序。 如果新的和旧行集重叠，则游标库可以通过重复使用行集缓冲区的重叠部分中的数据优化其性能。 因此，未保存的更改的行集缓冲区会丢失，除非新的和旧行集重叠，并且这些更改将行集缓冲区的重叠部分中。 若要保存所做的更改，应用程序提交定位的 update 语句。  
  
 请注意该游标库始终刷新缓存中的数据的行集缓冲区，当应用程序调用**SQLFetchScroll**与*FetchOrientation*参数设置为 SQL_FETCH_RELATIVE 和*FetchOffset*参数设置为 0。  
  
 游标库支持调用**SQLSetStmtAttr**与*属性*的 SQL_ATTR_ROW_ARRAY_SIZE 游标处于打开状态时更改的行集大小。 新的行集大小将会生效下次**SQLFetchScroll**调用。  
  
## <a name="result-set-membership"></a>结果集成员资格  
 仅在应用程序发出请求，该游标库从驱动程序检索数据。 具体取决于数据源和 SQL_CONCURRENCY 语句特性的设置，这会产生以下影响：  
  
-   检索由游标库的数据可能不同于在该语句的执行的时间都不可用的数据。 例如，打开游标后，可以通过某些驱动程序检索到一个点，在当前光标位置插入的行。  
  
-   结果集中的数据可能会锁定由游标库的数据源，因此在向其他用户不可用。  
  
 游标库已缓存了一行数据后，它无法检测 （除定位的更新和删除操作在同一个游标缓存上） 在基础数据源中的行进行更改。 这是因为，调用**SQLFetchScroll**，游标库永远不会 refetches 来自数据源的数据。 相反，它 refetches 其缓存中的数据。  
  
## <a name="scrolling"></a>滚动  
 游标库支持在以下的提取类型**SQLFetchScroll**。  
  
|游标类型|提取类型|  
|-----------------|-----------------|  
|只进|SQL_FETCH_NEXT|  
|Static|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>错误  
 当**SQLFetchScroll**调用，另一个对调用**SQLFetch**返回 SQL_ERROR，游标库将继续，如下所示。 完成这些步骤后，游标库将继续处理。  
  
1.  调用**SQLGetDiagRec**从驱动程序获取错误的信息并将此发布作为驱动程序管理器中的诊断记录。  
  
2.  SQL_DIAG_ROW_NUMBER 字段设置为适当的值的诊断记录。  
  
3.  如果适用; SQL_DIAG_COLUMN_NUMBER 字段设置为适当的值的诊断记录否则，它将其设置为 0。  
  
4.  设置中为 SQL_ROW_ERROR 行状态数组中的错误行的值。  
  
 光标位置后，库具有名为**SQLFetch**多次在其实现**SQLFetchScroll**，任何错误或警告返回到调用之一**SQLFetch**将在诊断记录，并可以通过调用来检索**SQLGetDiagRec**。 如果数据被截断时提取，截断的数据现在将驻留在游标库缓存中。 对后续调用**SQLFetchScroll**滚动到具有的行的截断的数据将返回截断的数据，并且会引发任何警告，因为从游标库缓存提取的数据。 若要跟踪的数据返回，以便它可以确定是否已截断的缓冲区中返回的数据的长度，应用程序应将绑定的长度/指示器缓冲区。  
  
## <a name="bookmark-operations"></a>书签操作  
 游标库支持调用**SQLFetchScroll**与*FetchOrientation*的 SQL_FETCH_BOOKMARK。 它还支持指定的偏移*FetchOffset*可以使用书签操作中的参数。 这是唯一的书签操作的游标库支持。 游标库不支持调用**SQLBulkOperations**。  
  
 如果应用程序已设置 SQL_ATTR_USE_BOOKMARKS 语句属性，并且已绑定到书签列，该游标库生成定长书签，并将其返回给应用程序。 游标库创建和维护的书签，它使用;它不使用维持在数据源的书签。 当**SQLFetchScroll**调用来检索已从数据源提取的数据块，它从游标库缓存中检索数据。 书签结果是，在调用中使用**SQLFetchScroll**与*FetchOrientation*的 SQL_FETCH_BOOKMARK 必须进行创建和维护由游标库。  
  
## <a name="interaction-with-other-functions"></a>与其他函数之间的交互  
 应用程序必须调用**SQLFetch**或**SQLFetchScroll**之前它准备或执行任何定位 update 或 delete 语句。
