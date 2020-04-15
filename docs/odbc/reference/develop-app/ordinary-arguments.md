---
title: 普通参数 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282458"
---
# <a name="ordinary-arguments"></a>普通自变量
当目录函数字符串参数是普通参数时，它被视为文本字符串。 普通参数既不接受字符串搜索模式，也不接受值列表。 普通参数的情况很重要，字符串中的报价字符是字面上的。 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_FALSE，则这些参数将被视为普通参数。如果此属性设置为SQL_TRUE，则它们将被视为标识符参数。  
  
 如果普通参数设置为空指针，并且参数是必需的参数，则函数将返回SQL_ERROR和 SQLSTATE HY009（无效使用空指针）。 如果普通参数设置为空指针，并且该参数不是必需的参数，则该参数的行为取决于驱动程序。 下表列出了所需的参数。  
  
|函数|必需参数|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*表名称*|  
|**SQLForeignKeys**|*PKTable 名称*， *FKTable 名称*|  
|**SQLPrimaryKeys**|*表名称*|  
|**SQLSpecialColumns**|*表名称*|  
|**SQLStatistics**|*表名称*|
