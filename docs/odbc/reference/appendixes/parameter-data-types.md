---
title: 参数数据类型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
manager: craigg
ms.openlocfilehash: e1f1097927f61355cf4a50f4287397d823fd3177
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632410"
---
# <a name="parameter-data-types"></a>参数数据类型
即使每个参数指定了**SQLBindParameter**是定义使用 SQL 数据类型，SQL 语句中的参数具有任何内部函数的数据类型。 因此，参数标记可以包含 SQL 语句中才可以从语句中的另一个操作数推断出其数据类型。 例如，在如算术表达式？ + 可以从 COLUMN1 所表示的命名列的数据类型推断出 COLUMN1，该参数的数据类型。 如果不确定的数据类型，应用程序不能使用参数标记。  
  
 下表介绍了几种类型的参数，根据 SQL-92 确定数据类型的方式。 在使用其他 SQL 子句时推断参数类型的更全面说明，请请参阅 SQL-92 规范。  
  
|参数的位置|假定数据类型|  
|---------------------------|-----------------------|  
|一个二元算术或比较运算符的操作数|与另一个操作数相同|  
|中的第一个操作数**BETWEEN**子句|第二个操作数相同|  
|中的第二个或第三个操作数**BETWEEN**子句|第一个操作数相同|  
|与所用的表达式**IN**|第一个值或子查询的结果列相同|  
|一个值，该值用于**IN**|表达式或表达式中的参数标记时的第一个值相同|  
|与使用的模式值**等**|VARCHAR|  
|与一起使用的更新值**更新**|更新列同名|
