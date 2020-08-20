---
description: 模式值自变量
title: 模式值参数 |Microsoft Docs
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
ms.openlocfilehash: a014c63c7fff6b82bbdd26d9fd5b4391c29d0ce2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465749"
---
# <a name="pattern-value-arguments"></a>模式值自变量
目录函数中的某些参数，如**SQLTables**中的*TableName*参数，接受搜索模式。 如果 SQL_ATTR_METADATA_ID 语句特性设置为 SQL_FALSE，则这些参数接受搜索模式;如果将此属性设置为 SQL_TRUE，它们是不接受搜索模式的标识符参数。  
  
 搜索模式字符如下：  
  
-   下划线 (_) ，表示任何单个字符。  
  
-   百分号 (% ) ，表示零个或多个字符的任意序列。  
  
-   转义符，它是特定于驱动程序的，用于将下划线、百分号和转义符作为文本包含。 如果转义符位于非特殊字符之前，则转义符没有特殊含义。 如果转义符位于特殊字符的前面，则它会转义特殊字符。 例如，可以将 "\a" 视为两个字符： " \\ " 和 "a"，但 " \\ %" 将被视为非特殊的单个字符 "%"。  
  
 用 **SQLGetInfo**中的 SQL_SEARCH_PATTERN_ESCAPE 选项检索转义字符。 它必须位于接受搜索模式的自变量中的任意下划线、百分号或转义符之前，才能将该字符作为文本包含。 下表显示了示例。  
  
|搜索模式|描述|  
|--------------------|-----------------|  
|的|包含字母 A 的所有标识符|  
|ABC_|以 ABC 开头的所有四个字符标识符|  
|ABC \\ _|标识符 ABC_，假设转义字符是反斜杠 (\\) |  
|\\\\%|以反斜杠开头的所有标识符 (\\) ，假设转义字符是反斜杠|  
  
 必须特别注意对接受搜索模式的参数中的搜索模式字符进行转义。 这对于下划线字符尤其适用，后者通常用于标识符。 应用程序中的一个常见错误是从一个目录函数检索一个值，并将该值传递到另一个目录函数中的搜索模式参数。 例如，假设应用程序从 **SQLTables** 的结果集中检索表名称 MY_TABLE，并将此名称传递给 **SQLColumns** 以检索 MY_TABLE 中的列的列表。 应用程序将获取与搜索模式 MY_TABLE 匹配的所有表的列，而不是获取 MY_TABLE 的列，如 MY_TABLE、MY1TABLE、MY2TABLE 等。  
  
> [!NOTE]
>  ODBC 2。*x*驱动程序不支持**SQLTables**中的*CatalogName*参数中的搜索模式。 如果 SQL_ATTR_ ODBC_VERSION 环境特性设置为 SQL_OV_ODBC3，则 ODBC*2.x 驱动程序* 接受此参数中的搜索模式;如果此参数设置为 SQL_OV_ODBC2，则不接受该参数中的搜索模式。  
  
 向搜索模式参数传递 null 指针不会限制该参数的搜索;也就是说，空指针和搜索模式% (任何) 等效的字符。 但是，长度为零的搜索模式（即指向长度为零的字符串的有效指针）仅匹配空字符串 ( "" ) 。
