---
title: 模式值自变量 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 53c091fd0b7a6cfdf390997fb5163fbc9d98e18c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023356"
---
# <a name="pattern-value-arguments"></a>模式值自变量
在目录中的某些参数函数，如*TableName*中的参数**SQLTables**，接受搜索模式。 这些参数接受搜索模式如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_FALSE;它们是如果此属性设置为 SQL_TRUE 不接受的搜索模式的标识符参数。  
  
 搜索模式字符包括：  
  
-   下划线 (_)，它表示任何单个字符。  
  
-   百分号 （%），它表示的零个或多个字符的任何序列。  
  
-   转义符，这是特定于驱动程序，用于包含下划线，百分比符号，并作为原义的转义字符。 如果非特殊字符的转义符前面，转义符将没有任何特殊的意义。 如果转义符之前都有特殊字符，它进行转义的特殊字符。 例如，"\a"将被视为两个字符"\\"和"a"，但"\\%"将被视为非特殊单个字符"%"。  
  
 使用中的 SQL_SEARCH_PATTERN_ESCAPE 选项检索的转义字符**SQLGetInfo**。 它必须位于任何下划线、 百分比符号或转义符之前接受搜索模式，以包含该字符作为文字的参数中。 下表显示示例。  
  
|搜索模式|描述|  
|--------------------|-----------------|  
|%A%|包含字母 A 的所有标识符|  
|ABC_|ABC 开头的所有四个字符标识符|  
|ABC\\_|标识符 ABC_，假设转义符是一个反斜杠 (\\)|  
|\\\\%|反斜杠开头的所有标识符 (\\)，假定转义符是一个反斜杠|  
  
 必须格外谨慎处理接受搜索模式的参数中的搜索模式字符进行转义。 这是对下划线字符，在标识符中通常使用而言尤其如此。 在应用程序中的一个常见错误是从一个目录函数中检索值并将该值传递到另一个目录函数中的搜索模式参数。 例如，假设应用程序中检索 MY_TABLE 从结果集的表名**SQLTables** ，并将传递到**SQLColumns**检索 MY_TABLE 中列的列表。 而不是获得 MY_TABLE 列，应用程序将获取与搜索模式 MY_TABLE MY_TABLE、 MY1TABLE、 MY2TABLE，等匹配的所有表的列。  
  
> [!NOTE]
>  ODBC 2。*x*驱动程序不支持中的搜索模式*CatalogName*中的参数**SQLTables**。 ODBC 3 *.x*驱动程序接受此参数中的搜索模式，如果 SQL_ATTR_ ODBC_VERSION 环境属性设置为 SQL_OV_ODBC3; 如果设置为 SQL_OV_ODBC2 不接受此参数中的搜索模式。  
  
 Null 指针传递给一个搜索模式参数将该自变量; 搜索不限制它是空指针，并且搜索模式 %（任何字符） 是等效的。 但是，长度为零的搜索模式-即，指向长度为零的字符串的有效指针的匹配只有空字符串 ("")。
