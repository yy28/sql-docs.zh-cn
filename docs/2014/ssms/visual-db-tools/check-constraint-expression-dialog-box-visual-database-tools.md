---
title: “CHECK 约束表达式”对话框 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.checkconstraintexpression
ms.assetid: beb6ce43-3913-4d66-8826-8e885335b790
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5e763c930a37e90d1bf23c186fa5db8a16c5e971
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63067883"
---
# <a name="check-constraint-expression-dialog-box-visual-database-tools"></a>“CHECK 约束表达式”对话框 (Visual Database Tools)
  向表或列附加 CHECK 约束时，必须包括 SQL 表达式。 在提供的框中键入 CHECK 约束表达式。  
  
## <a name="uielement-list"></a>UIElement 列表  
 表达式  
 输入表达式  
  
 您可以创建简单的约束表达式，用简单条件检查数据；也可以使用布尔运算符创建复杂表达式，用若干个条件检查数据。 例如，假设 Authors 表有一个需要 5 位数字字符串的邮政编码列。 下面的示例约束表达式可保证只允许 5 位的数字：  
  
```  
zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
```  
  
 或者，假设 sales 表中包含一个名为 qty 的列，此列的值必须大于 0。 此示例约束可保证只允许使用正值：  
  
```  
qty > 0  
```  
  
 或假设 Orders 表限制了所有信用卡订单可以接受的信用卡的类型。 下面的示例约束可保证在出现信用卡订单的情况下，只接受 Visa、MasterCard 或 American Express：  
  
```  
NOT (payment_method = 'credit card') OR  
   (card_type IN ('VISA', 'MASTERCARD', 'AMERICAN EXPRESS'))  
```  
  
## <a name="to-define-a-constraint-expression"></a>定义约束表达式  
 在属性页的“检查约束”选项卡中，使用以下语法在“约束表达式”框中键入表达式：  
  
 `{constant | column_name | function | (subquery)}`  
  
 `[{operator | AND | OR | NOT}`  
  
 `{constant | column_name | function | (subquery)}...]`  
  
 SQL 语法由下列参数组成：  
  
|参数|Description|  
|---------------|-----------------|  
|常量|一个如数值数据或字符数据之类的文本值。 字符数据必须用单引号 (') 括起来。|  
|column_name|指定列。|  
|函数|内置函数。|  
|运算符后的表达式|算术运算符、位运算符、比较运算符或字符串运算符。|  
|和|在布尔表达式中使用，用来连接两个表达式。 当两个表达式都为 True 时返回结果。<br /><br /> 当在一个语句中同时使用 AND 和 OR 时，首先处理 AND。 可以使用括号更改执行顺序。|  
|或|在布尔表达式中使用，用来连接两个或多个条件。 当任何一个条件为 True 时返回结果。<br /><br /> 当在一个语句中同时使用 AND 和 OR 时，在计算 AND 之后再计算 OR。 可以使用括号更改执行顺序。|  
|NOT|对任何布尔表达式（可包含如 LIKE、NULL、BETWEEN、IN 和 EXISTS 之类的关键字）求反。<br /><br /> 当在一个语句中使用多个逻辑运算符时，首先处理 NOT。 可以使用括号更改执行顺序。|  
  
## <a name="see-also"></a>请参阅  
 [唯一约束和 Check 约束](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [创建唯一约束](../../relational-databases/tables/create-unique-constraints.md)  
  
  
