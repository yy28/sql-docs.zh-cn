---
title: 模式值自变量 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39e6bf4734a63c79b09a78178e567900ff636bd3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="pattern-value-arguments"></a>模式值自变量
在目录中的某些参数函数，如*TableName*中的参数**SQLTables**，接受搜索模式。 这些自变量接受搜索模式如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_FALSE;它们是如果此属性设置为 SQL_TRUE 不接受的搜索模式的标识符参数。  
  
 搜索模式字符都是：  
  
-   下划线 (_)，它表示任何单个字符。  
  
-   百分号 （%），它表示的零个或多个字符的任何序列。  
  
-   转义符，这是特定于驱动程序，用于包含下划线，百分比符号，并为文本的转义字符。 如果转义字符之前的非特殊字符，转义字符都有没有特殊含义。 如果转义字符之前的特殊字符，它进行转义的特殊字符。 例如，"\a"将被视为两个字符，"\\"和"a"，但"\\%"将被视为非特殊单个字符"%"。  
  
 使用中的 SQL_SEARCH_PATTERN_ESCAPE 选项检索的转义字符**SQLGetInfo**。 它必须位于任何下划线、 百分号或转义字符之前在接受包含该字符作为文本的搜索模式的自变量。 下表显示了示例。  
  
|搜索模式|Description|  
|--------------------|-----------------|  
|%A%|包含字母 A 的所有标识符|  
|ABC_|所有四个字符标识符开头 ABC|  
|ABC\\_|ABC_，假设的转义字符的标识符包含一个反斜杠 (\\)|  
|\\\\%|所有标识符开头反斜杠 (\\)，假定转义字符包含一个反斜杠|  
  
 必须格外小心，接受搜索模式的自变量中的搜索模式字符进行转义。 这是对下划线字符，通常在标识符中使用而言尤其如此。 在应用程序中的一个常见错误是一个目录函数检索的值并将该值传递到另一个目录函数中的搜索模式参数。 例如，假设应用程序中检索 MY_TABLE 从结果设置为的表名**SQLTables**并将传递到**SQLColumns**检索 MY_TABLE 中的列列表。 而不是获取 MY_TABLE 列，应用程序将获取与搜索模式 MY_TABLE MY_TABLE、 MY1TABLE、 MY2TABLE，等匹配的所有表的列。  
  
> [!NOTE]  
>  ODBC 2。*x*驱动程序不支持中的搜索模式*CatalogName*中的参数**SQLTables**。 ODBC 3*.x*驱动程序接受此参数中的搜索模式，如果 SQL_ATTR_ ODBC_VERSION 环境属性设置为 SQL_OV_ODBC3; 如果设置为 SQL_OV_ODBC2 不接受此参数中的搜索模式。  
  
 将 null 指针传递给搜索 pattern 参数不限制该自变量; 搜索它是空指针，并且搜索模式 %（任何字符） 是等效的。 但是，长度为零的搜索模式-即，指向长度为零的字符串的有效指针-匹配仅空字符串 ("")。
