---
title: SQL 最小语法 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 4f36d785-104f-4fec-93be-f201203bc7c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20eee34feadb8e3140f25019ec6b0d036ff02e14
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304988"
---
# <a name="sql-minimum-grammar"></a>SQL 最低语法
本节介绍 ODBC 驱动程序必须支持的最低 SQL 语法。 本节中描述的语法是 SQL-92 的入门级语法的子集。  
  
 应用程序可以使用本节中的任何语法，并确保任何符合 ODBC 的驱动程序都将支持该语法。 要确定是否不支持本节中不支持 SQL-92 的其他功能，应用程序应使用SQL_SQL_CONFORMANCE信息类型调用**SQLGetInfo。** 即使驱动程序不符合任何 SQL-92 符合性级别，应用程序仍可以使用本节中描述的语法。 另一方面，如果驱动程序符合 SQL-92 级别，则驱动程序支持该级别中包含的所有语法。 这包括本节中的语法，因为此处描述的最小语法是最低 SQL-92 符合性级别的纯子集。 一旦应用程序知道 SQL-92 级别受支持，它可以通过调用**SQLGetInfo**与与该功能对应的单个信息类型来确定是否支持更高级别的功能（如果有）。  
  
 仅使用只读数据源的驱动程序可能不支持本节中有关更改数据的语法部分。 应用程序可以通过使用SQL_DATA_SOURCE_READ_ONLY信息类型调用**SQLGetInfo**来确定数据源是否为只读。  
  
## <a name="statement"></a>语句  
 *创建表语句*：：*  
  
 创建表*基表名称*  
  
 （*列标识符数据类型**=，列标识符数据类型**...  
  
> [!IMPORTANT]  
>  作为*创建表语句*中的*数据类型*，应用程序必须使用**SQLGetTypeInfo**返回的结果集TYPE_NAME列中的数据类型。  
  
 *删除语句搜索*：：*  
  
 从*表名中删除*[WHERE*搜索条件*]  
  
 *下拉表语句*：：*  
  
 DROP TABLE*基表名称*  
  
 *插入语句*：：*  
  
 插入表*名*[（*列标识符*[，*列标识符*]...）     值 （*插入值**，*插入值*#...  
  
 *select-statement* ::=  
  
 选择 [所有&#124; *select-list*  
  
 从*表引用列表*  
  
 [WHERE*搜索条件*]  
  
 [*逐项订购*]  
  
 *语句*：：**创建表语句*  
  
 &#124;*删除语句搜索*  
  
 &#124;*下表语句*  
  
 &#124;*插入语句*  
  
 &#124;*选择语句*  
  
 &#124;*更新语句搜索*  
  
 *更新语句搜索*  
  
 更新*表名称*  
  
 设置*列标识符*[ &#124;空*表达式*]  
  
 [，*列标识符*] [*表达式*&#124; NULL]...  
  
 [WHERE*搜索条件*]  
  
 本部分包含以下主题。  
  
-   [SQL 语句中使用的元素](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [数据类型支持](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [参数数据类型](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [参数标记](../../../odbc/reference/appendixes/parameter-markers.md)
