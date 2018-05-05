---
title: 书签类型 |Microsoft 文档
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
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06f720d61ae8be7b1a2c98ce2c749a4265e630d2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="bookmark-types"></a>书签类型
ODBC 3 中的所有书签 *.x*长度可变的书签。 这允许主键或唯一索引与表用作书签关联。 书签也可以为 32 位值，，ODBC 2 中使用的。*x*。 若要指定书签使用与某个游标，ODBC 3 *.x*应用程序将设置到 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARK 语句属性。 自动使用长度可变的书签。  
  
 应用程序可以调用**SQLColAttribute**与*FieldIdentifier*参数设置为 SQL_DESC_OCTET_LENGTH 若要获取书签的长度。 长度可变的书签可以为长整型值，因为应用程序应不绑定到列 0 除非将该书签用于许多在行集中的行。  
  
 固定长度书签仅支持向后兼容性。 如果检测到 ODBC 2。*x*应用程序使用 ODBC 3 *.x*驱动程序调用**SQLSetStmtOption**若要设置到 SQL_UB_ON SQL_USE_BOOKMARKS，它将映射 SQL_UB_VARIABLE 驱动程序管理器中. 将使用长度可变的书签，即使只有 32 位的它进行填充。 如果驱动程序支持固定长度书签，它将支持可变长度书签。 如果 ODBC 3 *.x*应用程序使用 ODBC 2。*x*驱动程序调用**SQLSetStmtAttr**若要设置到 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS，它映射 SQL_UB_ON 驱动程序管理器中，并用于 32 位固定长度书签。 SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性然后必须指向 32 位书签。 如果使用书签将变为超过 32 位，如主键时用作书签，光标必须映射到 32 位值的实际值。 例如，它可以生成它们的哈希表。 当 ODBC 3 *.x*应用程序使用 ODBC 2。*x*驱动程序绑定书签，缓冲区长度必须为 4。
