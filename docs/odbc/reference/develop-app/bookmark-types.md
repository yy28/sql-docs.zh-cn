---
title: 书签类型 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26d0297cd9dc57e9f30945a9248b235ae469da3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306328"
---
# <a name="bookmark-types"></a>书签类型
ODBC *3.x*中的所有书签都是可变长度的书签。 这允许将主键或与表关联的唯一索引用作书签。 书签也可以是 32 位值，如 ODBC *2.x*中使用的那样。 要指定书签与游标一起使用，ODBC *3.x*应用程序将SQL_ATTR_USE_BOOKMARK语句属性设置为SQL_UB_VARIABLE。 将自动使用可变长度书签。  
  
 应用程序可以调用**SQLColAttribute，** 字段*标识符*参数设置为SQL_DESC_OCTET_LENGTH以获取书签的长度。 由于可变长度书签可以是长值，因此应用程序不应绑定到列 0，除非它将对行集中的许多行使用书签。  
  
 固定长度书签仅支持向后兼容性。 如果使用 ODBC *3.x*驱动程序的 ODBC *2.x*应用程序调用**SQLSetStmtOption**将SQL_USE_BOOKMARKS设置为SQL_UB_ON，则它将在驱动程序管理器中映射到SQL_UB_VARIABLE。 使用可变长度书签，即使只填充了 32 位书签。 如果驱动程序支持固定长度书签，它将支持可变长度书签。 如果使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序调用**SQLSetStmtAttr**将SQL_ATTR_USE_BOOKMARKS设置为SQL_UB_VARIABLE，则它将在驱动程序管理器中映射到SQL_UB_ON，并且使用 32 位固定长度书签。 然后，SQL_ATTR_FETCH_BOOKMARK_PTR语句属性必须指向 32 位书签。 如果使用的书签长于 32 位（例如，当主键用作书签时）时，光标必须将实际值映射到 32 位值。 例如，它可以构建它们的哈希表。 当使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序绑定书签时，缓冲区长度必须为 4。
