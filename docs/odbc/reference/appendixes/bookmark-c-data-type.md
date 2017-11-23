---
title: "书签 C 数据类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 698e450fbb816c5fb7e3caf3786f4b8d469af50c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="bookmark-c-data-type"></a>书签 C 数据类型
书签 C 数据类型允许应用程序检索书签。 书签 C 类型仅用于检索书签可以是长度; 中的变量的值它们不应转换为其他数据类型。 应用程序中检索结果的第 0 列从设置的书签**SQLBulkOperations** （与 SQL_ADD 的操作）， **SQLFetch**， **SQLFetchScroll**，或**SQLGetData**。 有关详细信息，请参阅[书签](../../../odbc/reference/develop-app/bookmarks-odbc.md)。  
  
 下表列出的值*CType*实现书签 C 数据类型，以及此数据定义，则 ODBC C 数据类型从 SQL 对于书签 C 数据类型的类型。H。  
  
> [!NOTE]  
>  已弃用 SQL_C_BOOKMARK 数据类型。 ODBC 3*.x*应用程序不应使用 SQL_C_BOOKMARK。 ODBC 3*.x*驱动程序需要支持 SQL_C_BOOKMARK，仅当他们想要使用 ODBC 2。*x*使用它的应用程序。 当应用程序适用于 ODBC 2 时，驱动程序管理器映射到 SQL_C_BOOKMARK SQL_C_VARBOOKMARK。*x*驱动程序。  
  
|C 类型标识符|ODBC C typedef|C 类型|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />（不推荐使用）|书签|无符号长整数|  
|SQL_C_VARBOOKMARK|SQLCHAR *|无符号 char *|
