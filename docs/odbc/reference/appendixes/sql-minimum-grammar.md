---
title: SQL 最小语法 |Microsoft 文档
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
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 4f36d785-104f-4fec-93be-f201203bc7c7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3e31f53abf8d8788f719adc9e00e180ca7aa96f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909962"
---
# <a name="sql-minimum-grammar"></a>SQL 最小语法
本部分介绍 ODBC 驱动程序必须支持的最小 SQL 语法。 本节中所述的语法是 SQL 92 条目级别语法的子集。  
  
 应用程序可以使用任何语法在本部分中，并确保任何符合 ODBC 的驱动程序将支持该语法。 若要确定是否支持 sql-92 不在本部分中的附加功能，应用程序应调用**SQLGetInfo** SQL_SQL_CONFORMANCE 信息类型。 即使该驱动程序不符合到任何 SQL 92 一致性级别时，应用程序仍可以使用本部分中描述的语法。 如果驱动程序符合 SQL 92 级别，另一方面，它支持在该级别中包含的所有语法。 这在本部分包括语法，因为此处所述的最小语法是纯最低的 SQL 92 一致性级别的子集。 一旦应用程序知道支持的 SQL 92 级别，它可以确定是否更高级别的功能支持 （是否有） 通过调用**SQLGetInfo**与对应于该功能的单独的信息类型。  
  
 只能使用只读的数据源的驱动程序可能不支持语法包括在本部分处理的更改数据的那些的部分。 应用程序可以确定数据源通过调用是否是只读的**SQLGetInfo** SQL_DATA_SOURCE_READ_ONLY 信息类型。  
  
## <a name="statement"></a>。  
 *创建 table 语句*:: =  
  
 CREATE TABLE*基本表名称*  
  
 (*列标识符数据类型*[*，列标识符数据类型*]...)  
  
> [!IMPORTANT]  
>  作为*数据类型*中*创建 table 语句*，应用程序必须使用从 TYPE_NAME 列数据类型为返回的结果集**SQLGetTypeInfo**。  
  
 *delete 语句搜索*:: =  
  
 DELETE FROM*表名*[其中*搜索条件*]  
  
 *drop table 语句*:: =  
  
 DROP TABLE*基本表名称*  
  
 *insert 语句*:: =  
  
 INSERT INTO*表名*[(*列标识符*[，*列标识符*]...)]     值 (*插入值*[，*插入值*]...)  
  
 *选择语句*:: =  
  
 选择 [所有&#124;DISTINCT]*选择列表*  
  
 从*表引用列表*  
  
 [其中*搜索条件*]  
  
 [*order by 子句*]  
  
 *语句*:: =*创建 table 语句*  
  
 &#124;*delete 语句搜索*  
  
 &#124;*drop table 语句*  
  
 &#124;*insert 语句*  
  
 &#124;*选择语句*  
  
 &#124;*更新语句搜索*  
  
 *更新语句搜索*  
  
 更新*表名称*  
  
 设置*列标识符*= {*表达式* &#124; NULL}  
  
 [，*列标识符*= {*表达式* &#124; NULL}]...  
  
 [其中*搜索条件*]  
  
 本部分包含以下主题。  
  
-   [SQL 语句中使用的元素](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [数据类型支持](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [参数数据类型](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [参数标记](../../../odbc/reference/appendixes/parameter-markers.md)
