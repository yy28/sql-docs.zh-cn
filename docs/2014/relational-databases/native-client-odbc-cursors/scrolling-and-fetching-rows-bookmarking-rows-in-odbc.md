---
title: 书签 ODBC 中的行 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- ODBC cursors, scrolling rows
- bookmarks [ODBC]
ms.assetid: 9cfcd243-c9d4-4c2a-abc4-399dbabe5f6b
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7f2d19fe6cf79e11c11a5e6c5c4839ae35788353
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025472"
---
# <a name="bookmarking-rows-in-odbc"></a>在 ODBC 中为行加书签
  书签是用于标识数据行的值。 只有驱动程序或数据源才知道书签值的含义。 例如，书签可能与行号一样简单，也可能与磁盘地址一样复杂。 在 ODBC 中，应用程序为特定行请求书签，存储该书签，并将其传回到游标以返回到该行。  
  
 在提取的行时[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)，应用程序可以将书签用作基础用于选择的起始行。 这是一种绝对寻址的格式，因为它不依赖于当前游标位置。 要滚动到书签的行，则应用程序调用**SQLFetchScroll**与*FetchOrientation* SQL_FETCH_BOOKMARK。 此操作使用 SQL_ATTR_FETCH_BOOKMARK_PTR 选项属性所指向的书签。 它将返回以该书签标识的行开始的行集。 应用程序可以指定在此操作的偏移量*FetchOffset*到调用自变量**SQLFetchScroll**。 指定偏移量后，会通过将 FetchOffset 参数中的数字与由书签标识的这一行的编号相加来确定所返回行集的第一行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序只对于静态游标和键集游标支持书签。 如果在设置书签时要求动态游标，则转而打开键集游标。  
  
 此外可以与使用书签**SQLBulkOperations**函数在一组开始书签的行上执行操作。  
  
## <a name="see-also"></a>请参阅  
 [滚动和提取行](../native-client-ole-db-rowsets/fetching-rows.md)  
  
  