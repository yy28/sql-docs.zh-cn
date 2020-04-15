---
title: 模式值参数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b8e7b7de64d8051118089a54cf14eb45dc96f74
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282377"
---
# <a name="pattern-value-arguments"></a>模式值自变量
目录函数中的某些参数（如**SQLTables**中的*表名称*参数）接受搜索模式。 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_FALSE，则这些参数接受搜索模式;如果此属性设置为SQL_TRUE，它们是不接受搜索模式的标识符参数。  
  
 搜索模式字符为：  
  
-   表示任何单个字符的下划线 （*）。  
  
-   百分比符号 （%），表示任何零个或多个字符序列。  
  
-   转义字符，它是特定于驱动程序的，用于将下划线、百分比符号和转义字符作为文本。 如果转义字符位于非特殊字符之前，则转义字符没有特殊含义。 如果转义字符位于特殊字符前面，则它将转义特殊字符。 例如，"\a"将被视为两个字符""\\和"a"，但"%"\\将被视为非特殊单个字符"%"。  
  
 转义符使用**SQLGetInfo**中的SQL_SEARCH_PATTERN_ESCAPE选项进行检索。 它必须位于接受搜索模式的参数中的任何下划线、百分比符号或转义字符之前，才能将该字符作为文本包含。 下表中显示了示例。  
  
|搜索模式|描述|  
|--------------------|-----------------|  
|%A%|包含字母 A 的所有标识符|  
|ABC_|所有四个字符标识符以 ABC 开头|  
|ABC\\||标识符ABC_，假设转义字符是反斜杠 （\\）|  
|\\\\%|假定转义字符是反斜杠，\\则以反斜杠 （） 开头的所有标识符|  
  
 必须特别注意在接受搜索模式的参数中转义搜索模式字符。 对于标识符中常用的下划线字符尤其如此。 应用程序中的一个常见错误是从一个目录函数中检索值，并将该值传递给另一个目录函数中的搜索模式参数。 例如，假设应用程序从**SQLTables**的结果集中检索表名称MY_TABLE并将其传递给**SQLColumns**以检索MY_TABLE中的列列表。 应用程序将获取与搜索模式匹配的所有表的列，MY_TABLE（如MY_TABLE、MY1TABLE、MY2TABLE 等）而不是获取MY_TABLE列。  
  
> [!NOTE]
>  ODBC 2.*x*驱动程序不支持**SQLTables**中的*目录名称*参数中的搜索模式。 如果SQL_ATTR_ODBC_VERSION环境属性设置为SQL_OV_ODBC3，则 ODBC 3 *.x*驱动程序在此参数中接受搜索模式;如果搜索模式设置为SQL_OV_ODBC2，则不接受此参数中的搜索模式。  
  
 将空指针传递给搜索模式参数不会限制该参数的搜索;因此，将空指针传递给搜索模式参数。也就是说，空指针和搜索模式 % （任何字符） 是等效的。 但是，零长度搜索模式（即指向长度为零的字符串的有效指针）仅匹配空字符串 （""）。
