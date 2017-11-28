---
title: "参数数据类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 655868b77b482a11145e8947e1ea81d34270ca65
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
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
