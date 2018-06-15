---
title: SQLFetchScroll （光标库） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLFetchScroll function [ODBC], Cursor Library
ms.assetid: 4417e57c-31dd-475e-8fe9-eab00a459c80
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0c3e9709cd3aeced11116ab88c5323d4462abd2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914072"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLFetchScroll**光标库中的函数。 有关常规信息**SQLFetchScroll**，请参阅[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
 游标库实现**SQLFetchScroll**通过反复调用**SQLFetch**驱动程序中。 它将它从驱动程序将检索到应用程序提供的行集缓冲区数据传输。 它还将缓存内存和磁盘的文件中的数据。 当应用程序请求一个新行集时，游标库检索它根据需要从驱动程序 （如果它不被以前取回） 或缓存 （如果它具有以前提取）。 最后，光标库维护缓存的数据的状态，并返回到行状态数组中的应用程序的此信息。  
  
 当使用的是光标库时，调用**SQLFetchScroll**不能与调用混合**SQLFetch**或**SQLExtendedFetch**。  
  
 当使用的是光标库时，调用**SQLFetchScroll**是支持的 ODBC 2。*x*和适用于 ODBC 3。*x*驱动程序。  
  
## <a name="rowset-buffers"></a>行集缓冲区  
 游标库优化数据驱动程序传输到如果应用程序提供的行集缓冲区：  
  
-   应用程序使用按行绑定。  
  
-   中的应用程序声明来保存数据行的结构字段之间有任何未使用的字节。  
  
-   在其中的字段**SQLFetch**或**SQLFetchScroll**对一个列遵循该列的缓冲区和之前的缓冲区的下一列都返回长度/指示器。 这些字段是可选的。  
  
 当应用程序请求一个新行集时，游标库中从其缓存和根据需要的驱动程序检索数据。 如果新和旧行集重叠，光标库可通过重复使用的行集缓冲区的重叠部分中的数据优化其性能。 因此，行集的缓冲区的未保存的更改将丢失，除非新和旧行集重叠，并且所做的更改的行集缓冲区重叠部分中。 若要保存所做的更改，应用程序，请提交定位的 update 语句。  
  
 请注意的是光标库始终刷新缓存中的数据的行集缓冲区，当应用程序调用**SQLFetchScroll**与*FetchOrientation*参数设置为 SQL_FETCH_RELATIVE 和*FetchOffset*参数设置为 0。  
  
 游标库支持调用**SQLSetStmtAttr**与*属性*的 SQL_ATTR_ROW_ARRAY_SIZE 游标处于打开状态时更改的行集大小。 新的行集大小将会生效的下一步时间**SQLFetchScroll**调用。  
  
## <a name="result-set-membership"></a>结果集成员身份  
 仅在应用程序请求它，光标库的驱动程序中检索数据。 根据数据源和 SQL_CONCURRENCY 语句特性的设置，这样做有以下结果：  
  
-   检索由游标库的数据可能会与不同的数据时可用的已执行语句的时间。 例如，打开游标后，可以通过某些驱动程序检索在超出当前光标位置的某个点处插入的行。  
  
-   在结果集中的数据可能锁定的是光标库的数据源，，因此是不能供其他用户。  
  
 游标库已缓存数据行后，它无法在基础数据源 （除外定位的更新和删除操作在同一游标缓存上） 中检测到该行的更改。 这是因为，以便调用**SQLFetchScroll**，光标库永远不会 refetches 来自数据源的数据。 相反，它 refetches 从其缓存的数据。  
  
## <a name="scrolling"></a>滚动  
 游标库支持中的以下提取类型**SQLFetchScroll**。  
  
|游标类型|提取类型|  
|-----------------|-----------------|  
|只进|SQL_FETCH_NEXT|  
|静态|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>错误  
 当**SQLFetchScroll**称为，另一个对的调用**SQLFetch**返回 SQL_ERROR，光标库将继续，如下所示。 完成这些步骤后，光标库将继续处理。  
  
1.  调用**SQLGetDiagRec**以获取从驱动程序的错误信息并将此作为诊断记录在驱动程序管理器中。  
  
2.  设置 SQL_DIAG_ROW_NUMBER 字段中为适当的值的诊断记录。  
  
3.  SQL_DIAG_COLUMN_NUMBER 字段设置为适当的值，诊断记录中，如果适用;否则，它将其设置为 0。  
  
4.  到 SQL_ROW_ERROR 行状态数组中的错误中设置行的值。  
  
 光标位置后库已调用**SQLFetch**多次在其实现**SQLFetchScroll**，任何错误或警告返回到调用之一**SQLFetch**将诊断记录中，可以通过调用检索**SQLGetDiagRec**。 如果数据被截断时提取，截断的数据将现在驻留在光标库的缓存中。 后续调用**SQLFetchScroll**要滚动到某一行而该行截断的数据将返回的截断的数据，并且将会引发任何警告，因为从光标库的缓存中提取数据。 若要跟踪的返回，以便它能够确定是否在缓冲区中返回的数据已被截断的数据的长度，应用程序应将绑定的长度/指示器缓冲区。  
  
## <a name="bookmark-operations"></a>书签操作  
 游标库支持调用**SQLFetchScroll**与*FetchOrientation* SQL_FETCH_BOOKMARK。 它还支持指定中的偏移量*FetchOffset*可在书签操作的自变量。 这是光标库支持仅有书签的操作。 游标库不支持调用**SQLBulkOperations**。  
  
 如果应用程序已设置 SQL_ATTR_USE_BOOKMARKS 语句属性，并且已绑定到书签列，光标库生成固定长度书签，并将其返回给应用程序。 游标库创建和维护它使用; 在书签它不使用维持在数据源的书签。 当**SQLFetchScroll**称为若要检索的尚未从数据源获取的数据块，它从光标库缓存中检索数据。 书签结果是，对的调用中使用**SQLFetchScroll**与*FetchOrientation*的 SQL_FETCH_BOOKMARK 必须可由创建和维护的是光标库。  
  
## <a name="interaction-with-other-functions"></a>与其他函数之间的交互  
 应用程序必须调用**SQLFetch**或**SQLFetchScroll**它准备或执行之前任何定位更新或删除语句。
