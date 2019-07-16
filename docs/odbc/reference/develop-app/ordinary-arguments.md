---
title: 普通自变量 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 997604b4376656d36d2bc4bc31f1959aa6c8a229
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987829"
---
# <a name="ordinary-arguments"></a>普通自变量
目录函数字符串自变量时的普通参数，则将它视为文本字符串。 普通参数接受字符串的搜索模式既不值的列表。 普通自变量的情况是有意义的并在字符串中的引号字符将按字面解释。 这些参数将被视为普通自变量，如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_FALSE;它们被视为标识符参数改为如果此属性设置为 SQL_TRUE。  
  
 如果参数是必需的参数的普通参数设置为 null 指针，该函数返回 SQL_ERROR 并且 SQLSTATE HY009 （null 指针的使用无效）。 如果普通参数设置为 null 指针，该参数不是必需的参数，参数的行为是依赖于驱动程序的。 下表中列出所需的参数。  
  
|函数|所需的参数|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*， *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
