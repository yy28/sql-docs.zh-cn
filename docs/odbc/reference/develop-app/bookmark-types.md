---
title: 书签类型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb8f5848ef9fdffab8592215fdcc5406b24319c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118781"
---
# <a name="bookmark-types"></a>书签类型
*ODBC 3.x 中的所有*书签均为可变长度书签。 这允许将与表关联的主键或唯一索引用作书签。 书签还可以是一个32位值，与 ODBC 2.x 中使用的值*相同。* 若要指定书签与光标一起使用 *，ODBC 3.x*应用程序将 SQL_ATTR_USE_BOOKMARK 语句特性设置为 SQL_UB_VARIABLE。 自动使用变长书签。  
  
 应用程序可以调用**SQLColAttribute** ，并将*FieldIdentifier*参数设置为 SQL_DESC_OCTET_LENGTH 以获取书签的长度。 由于可变长度书签可以是长值，因此应用程序不应绑定到列0，除非它将为行集中的许多行使用书签。  
  
 支持固定长度书签，只是为了向后兼容。 如果使用 ODBC *1.x 驱动程序的 odbc* 1.x 应用程序调用**SQLSetStmtOption**将 SQL_USE_BOOKMARKS 设置为 SQL_UB_ON，则该*应用程序会*在驱动程序管理器中进行映射，以便 SQL_UB_VARIABLE。 使用变长书签，即使只填充了32位。 如果驱动程序支持固定长度书签，则它将支持可变长度书签。 如果使用 ODBC *2.x 驱动程序的 odbc* 1.x 应用程序调用**SQLSetStmtAttr**将 SQL_ATTR_USE_BOOKMARKS 设置为 SQL_UB_VARIABLE，则该*应用程序会*在驱动程序管理器中映射到，SQL_UB_ON 并使用32位固定长度书签。 然后，SQL_ATTR_FETCH_BOOKMARK_PTR 语句特性必须指向32位书签。 如果使用的书签超过32位（例如，当主键用作书签时），则游标必须将实际值映射到32位值。 例如，可以生成一个哈希表。 当使用 ODBC 2.x*驱动程序的 odbc* *1.x 应用程序*绑定书签时，缓冲区长度必须为4。
