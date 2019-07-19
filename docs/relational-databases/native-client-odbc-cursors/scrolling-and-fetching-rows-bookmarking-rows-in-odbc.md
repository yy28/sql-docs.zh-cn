---
title: 在 ODBC 中为行加书签 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- ODBC cursors, scrolling rows
- bookmarks [ODBC]
ms.assetid: 9cfcd243-c9d4-4c2a-abc4-399dbabe5f6b
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 40180e8f2fe9b4f77546dd95da1813eec6ce1f96
ms.sourcegitcommit: 3be14342afd792ff201166e6daccc529c767f02b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68078825"
---
# <a name="scrolling-and-fetching-rows---bookmarking-rows-in-odbc"></a>滚动和提取行 - 在 ODBC 中为行加书签
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  书签是用于标识数据行的值。 只有驱动程序或数据源才知道书签值的含义。 例如，书签可能与行号一样简单，也可能与磁盘地址一样复杂。 在 ODBC 中，应用程序为特定行请求书签，存储该书签，并将其传回到游标以返回到该行。  
  
 使用[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)提取行时, 应用程序可以使用书签作为选择起始行的基础。 这是一种绝对寻址的格式，因为它不依赖于当前游标位置。 若要滚动到带有书签的行, 应用程序将使用 SQL_FETCH_BOOKMARK 的*FetchOrientation*调用**SQLFetchScroll** 。 此操作使用 SQL_ATTR_FETCH_BOOKMARK_PTR 选项属性所指向的书签。 它将返回以该书签标识的行开始的行集。 应用程序可以在调用**SQLFetchScroll**的*FetchOffset*参数中指定此操作的偏移量。 指定偏移量后，会通过将 FetchOffset 参数中的数字与由书签标识的这一行的编号相加来确定所返回行集的第一行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序只对于静态游标和键集游标支持书签。 如果在设置书签时要求动态游标，则转而打开键集游标。  
  
 书签还可与**SQLBulkOperations**函数一起使用, 以便对一组从书签开始的行执行操作。  
  
## <a name="see-also"></a>请参阅  
 [滚动和提取行](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
  
