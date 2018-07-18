---
title: 普通自变量 |Microsoft 文档
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
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ecdcf5e697bcf3235cadbe3d8f3f8f981406575
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911642"
---
# <a name="ordinary-arguments"></a>普通自变量
时的目录函数字符串自变量是的普通自变量，它将被视为文字字符串。 普通参数接受字符串的搜索模式和的值列表都不。 普通自变量的情况是有意义的并按原义转字符串中的引号字符。 这些自变量被视为普通自变量，如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_FALSE;将它们视为标识符自变量而是如果此属性设置为 SQL_TRUE。  
  
 如果普通自变量设置为 null 指针并且参数是一个必需的参数，则函数返回 SQL_ERROR 和 SQLSTATE HY009 （不允许使用 null 指针）。 如果普通自变量设置为 null 指针并且的参数不是必需的自变量，自变量的行为不依赖于驱动程序的。 下表中列出所需的参数。  
  
|函数|所需的参数|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*， *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
