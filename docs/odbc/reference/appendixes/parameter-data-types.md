---
title: 参数数据类型 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a43fdab2fd7ffeaf409bde41c06386fad23d3c3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="parameter-data-types"></a>参数数据类型
即使每个参数指定与**SQLBindParameter**是定义使用 SQL 数据类型，SQL 语句中的参数具有任何内部函数的数据类型。 因此，参数标记可以包含在 SQL 语句才可以从语句中的另一个操作数推断其数据类型。 例如，在如算术表达式？ + 可以从 COLUMN1 所表示的指定列的数据类型推断出 COLUMN1，参数的数据类型。 如果无法确定的数据类型，应用程序无法使用参数标记。  
  
 下表介绍几种类型的参数，根据 SQL 92 确定一种数据类型的方式。 在推断更全面规范的参数类型时使用其他 SQL 子句，请参阅 SQL 92 规范。  
  
|参数的位置|假定数据类型|  
|---------------------------|-----------------------|  
|一个二进制算术或比较运算符的操作数|与另一个操作数相同|  
|中的第一个操作数**BETWEEN**子句|第二个操作数相同|  
|中的第二个或第三个操作数**BETWEEN**子句|第一个操作数相同|  
|与所用的表达式**IN**|第一个值或子查询的结果列相同|  
|用于值**IN**|表达式或表达式中参数标记时的第一个值相同|  
|与使用一个模式值**如**|VARCHAR|  
|用于更新值**更新**|更新列相同|
