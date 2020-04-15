---
title: 参数数据类型 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: f29bb70937df32e03480c13c7ef739eb273f15eb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303578"
---
# <a name="parameter-data-types"></a>参数数据类型
即使使用**SQLBind 参数**指定的每个参数都是使用 SQL 数据类型定义的，但 SQL 语句中的参数没有内在数据类型。 因此，仅当参数标记的数据类型可以从语句中的另一个操作数推断出来时，才能包含在 SQL 语句中。 例如，在算术表达式中，如 ？ • COLUMN1，可以从 COLUMN1 表示的命名列的数据类型推断参数的数据类型。 如果无法确定数据类型，则应用程序无法使用参数标记。  
  
 下表描述了如何根据 SQL-92 确定多种类型的参数的数据类型。 有关在使用其他 SQL 子句时推断参数类型的更全面的规范，请参阅 SQL-92 规范。  
  
|参数的位置|假定数据类型|  
|---------------------------|-----------------------|  
|二进制算术或比较运算符的一个操作数|与其他操作数相同|  
|**在"之间"** 子句中的第一个操作数|与第二个操作数相同|  
|**在 BETWEEN**子句中的第二个或第三个操作数|与第一个操作数相同|  
|与**IN**一起使用的表达式|与子查询的第一个值或结果列相同|  
|与**IN**一起使用的值|如果表达式中有参数标记，则与表达式或第一个值相同|  
|与**LIKE**一起使用的模式值|VARCHAR|  
|与**更新**一起使用的更新值|与更新列相同|
