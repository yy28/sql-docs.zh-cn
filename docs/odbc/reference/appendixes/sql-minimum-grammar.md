---
title: SQL 最低语法 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85b1f59efd809c604458bd7b99882705db240e9a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057007"
---
# <a name="sql-minimum-grammar"></a>SQL 最低语法
本部分介绍的 ODBC 驱动程序必须支持的最小 SQL 语法。 在本部分中所述的语法是 SQL-92 的条目级别语法的子集。  
  
 应用程序可以使用任何语法在本部分中，并确保任何符合 ODBC 驱动程序将支持该语法。 若要确定是否支持 SQL-92 不在本部分中的其他功能，应用程序应调用**SQLGetInfo** SQL_SQL_CONFORMANCE 信息类型。 即使该驱动程序不符合任何 SQL-92 的一致性级别，应用程序仍可以使用本部分中描述的语法。 如果驱动程序符合 SQL-92 级别，但是，它支持在该级别中包含的所有语法。 这在本部分中包含的语法，因为此处所述的最小语法是纯的最低 SQL-92 符合性级别的子集。 一旦应用程序知道支持的 SQL-92 级别，它可以确定是否支持某一更高级别的功能是 （是否有） 通过调用**SQLGetInfo**与对应于该功能的单个信息类型。  
  
 仅使用只读数据源的驱动程序可能不支持此部分中包含的语法处理变化的数据的那些的部分。 应用程序可以确定数据源通过调用是否是只读**SQLGetInfo** SQL_DATA_SOURCE_READ_ONLY 信息类型。  
  
## <a name="statement"></a>声明专用纸  
 *create table 语句*:: =  
  
 CREATE TABLE*基础表名称*  
  
 (*数据类型列标识符*[ *，列标识符的数据类型*]...)  
  
> [!IMPORTANT]  
>  作为*数据类型*中*create table 语句*，应用程序必须使用返回的结果集的 TYPE_NAME 列中数据类型**SQLGetTypeInfo**。  
  
 *delete 语句搜索*:: =  
  
 DELETE FROM *l e-n* [其中*搜索条件*]  
  
 *drop table 语句*:: =  
  
 DROP TABLE*基础表名称*  
  
 *insert 语句*:: =  
  
 INSERT INTO *l e-n* [(*列标识符*[，*列标识符*]...)]     值 (*插入值*[， *insert 值*]...)  
  
 *选择语句*:: =  
  
 选择 [所有&#124;DISTINCT]*选择列表*  
  
 从*表引用列表*  
  
 [其中*搜索条件*]  
  
 [*order-by-clause*]  
  
 *语句*:: = *create table 语句*  
  
 &#124;*delete 语句搜索*  
  
 &#124; *drop-table-statement*  
  
 &#124; *insert-statement*  
  
 &#124;*select 语句*  
  
 &#124; *update-statement-searched*  
  
 *update-statement-searched*  
  
 更新*表名称*  
  
 设置*列标识符*= {*表达式* &#124; NULL}  
  
 [，*列标识符*= {*表达式* &#124; NULL}]...  
  
 [其中*搜索条件*]  
  
 本部分包含以下主题。  
  
-   [SQL 语句中使用的元素](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [数据类型支持](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [参数数据类型](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [参数标记](../../../odbc/reference/appendixes/parameter-markers.md)
