---
title: 普通参数 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97362f93e91ccd8b592b4c05a0714b7602c1ba94
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282458"
---
# <a name="ordinary-arguments"></a>普通自变量
如果目录函数字符串参数是普通参数，则将其视为文本字符串。 普通参数既不接受字符串搜索模式，也不接受值列表。 普通参数的大小写很重要，字符串中的引号字符将按原义提取。 如果 SQL_ATTR_METADATA_ID 语句特性设置为 SQL_FALSE，则这些参数被视为普通参数;如果将此属性设置为 SQL_TRUE，则将它们视为标识符参数。  
  
 如果普通参数设置为 null 指针，并且该参数是必需参数，则函数将返回 SQL_ERROR 和 SQLSTATE HY009 （null 指针的使用无效）。 如果普通参数设置为 null 指针，并且参数不是必需参数，则参数的行为取决于驱动程序。 下表列出了所需的参数。  
  
|函数|必需的参数|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*、 *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
