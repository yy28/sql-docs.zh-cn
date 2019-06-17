---
title: 书签 C 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b81acf6c60bd11e03a598e349e145dbf72e174b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026952"
---
# <a name="bookmark-c-data-type"></a>书签 C 数据类型
书签 C 数据类型允许应用程序来检索一个书签。 书签 C 类型仅用于检索可以是变量的长度; 的书签值它们不应转换为其他数据类型。 应用程序将检索从第 0 列的结果与设置的书签**SQLBulkOperations** （带有 SQL_ADD 的操作）， **SQLFetch**， **SQLFetchScroll**，或**SQLGetData**。 有关详细信息，请参阅[书签](../../../odbc/reference/develop-app/bookmarks-odbc.md)。  
  
 下表列出的值*CType*书签 C 数据类型中，键入从 SQL 实现书签 C 数据类型，并且此类数据定义的 ODBC C 数据类型。H.  
  
> [!NOTE]
>  已弃用 SQL_C_BOOKMARK 数据类型。 ODBC 3 *.x*应用程序不应使用 SQL_C_BOOKMARK。 ODBC 3 *.x*驱动程序需要仅当他们想要使用 ODBC 2 支持 SQL_C_BOOKMARK。*x*使用它的应用程序。 当应用程序适用于 ODBC 2 时，驱动程序管理器映射到 SQL_C_BOOKMARK SQL_C_VARBOOKMARK。*x*驱动程序。  
  
|C 类型标识符|ODBC C typedef|C 类型|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />（不推荐使用）|书签|无符号长整型|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|
