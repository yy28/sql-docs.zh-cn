---
title: "精度、 小数位数和长度 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], length
- data types [SQL Server], scale
- precision [SQL Server], data types
- lengths [SQL Server], data types
- number of digits
- scale [SQL Server]
- scale [SQL Server], data types
- data types [SQL Server], precision
ms.assetid: fbc9ad2c-0d3b-4e98-8fdd-4d912328e40a
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 557d7a5c45e9cc5a0839dfb4a1fdb0d08c2bf83f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="precision-scale-and-length-transact-sql"></a>精度、 小数位数和长度 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

精度指数字的位数。 小数位数指小数点后的数字位数。 例如，数 123.45 的精度是 5，小数位数是 2。
  
在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的默认最大精度**数值**和**十进制**数据类型为 38。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本中，默认最大精度为 28。
  
数字数据类型的长度是存储此数所占用的字节数。 字符串或 Unicode 数据类型的长度是字符个数。 长度**二进制**， **varbinary**，和**映像**数据类型是的字节数。 例如， **int**数据类型可以有 10 位数，存储在 4 个字节，而不接受位小数。 **Int**数据类型具有精度为 10，（4)，长度和小数位数为 0。
  
当两个**char**， **varchar**，**二进制**，或**varbinary**表达式串联在一起，生成的表达式的长度为两个源表达式或 8000 个字符，长度的总和小者为准。
  
当两个**nchar**或**nvarchar**表达式串联在一起，生成的表达式的长度是两个源表达式或 4000 个字符的长度的总和小者为准。
  
使用 UNION、EXCEPT 或 INTERSECT 对数据类型相同但长度不同的两个表达式进行比较时，得到的长度为两个表达式中较大的长度。
  
精度和小数位数的数值数据类型，除了**十进制**固定的。 如果算术运算符有两个相同类型的表达式，结果就为该数据类型，并且具有对此类型定义的精度和小数位数。 如果运算符有两个不同数字数据类型的表达式，则由数据类型优先级决定结果的数据类型。 结果具有为该数据类型定义的精度和小数位数。
  
下表定义的类型的操作的结果时的精度和小数位数结果如何计算**十进制**。 结果是**十进制**满足以下任一时：
-   两个表达式均**十进制**。  
-   一个表达式是**十进制**，另一个是一个较低优先级的数据类型**十进制**。  
  
操作数表达式由表达式 e1（精度为 p1，小数位数为 s1）和表达式 e2（精度为 p2，小数位数为 s2）来表示。 精度和小数位数不是任何表达式**十进制**是精度和小数位数为表达式的数据类型定义。
  
|运算|结果精度|结果小数位数 *|  
|---|---|---|
|e1 + e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 - e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 * e2|p1 + p2 + 1|s1 + s2|  
|e1 / e2|p1 - s1 + s2 + max(6, s1 + p2 + 1)|max(6, s1 + p2 + 1)|  
|e1 {联合 &#124; 除 &#124; INTERSECT} e2|max(s1, s2) + max(p1-s1, p2-s2)|max(s1, s2)|  
|e1 % e2|min(p1-s1, p2 -s2) + max( s1,s2 )|max(s1, s2)|  
  
\*结果精度和小数位数具有 38 一个绝对上限值。 在结果精度大于 38，将其减少为 38，而对相应刻度则降低尝试以防止结果的整数部分被截断。 在如乘法或除法某些情况下，缩放比例将不会减少为了使小数精度，尽管可以引发溢出错误。

在加法和减法运算中，我们将需要`max(p1 – s1, p2 – s2)`存储的十进制数的组成部分的位置。 如果没有足够空间来存储它们即`max(p1 – s1, p2 – s2) < min(38, precision) – scale`，小数位数会减少为组成部分提供足够的空间。 生成的小数位数是`MIN(precision, 38) - max(p1 – s1, p2 – s2)`，因此可能舍入的小数部分，使其适合生成缩放。

乘法和除法操作中，我们需要`precision - scale`存储结果的整数部分的位置。 小数位数可能会降低，使用以下规则：
1.  生成的比例减少到`min(scale, 38 – (precision-scale))`的整数部分是否小于 32、，因为它不能大于`38 – (precision-scale)`。 结果可能会在这种情况下舍入。
1. 如果它是小于 6 和的整数部分大于 32，缩放将不会更改。 如果它无法放入 decimal （38，缩放） 在这种情况下，可能引发溢出错误 
1. 如果该长度超过 6 和的整数部分大于 32，刻度将设置为 6。 在这种情况下，将减少的整数部分和缩放，并且生成的类型是 decimal(38,6)。 结果可能舍入为 6 的小数位数，否则将引发溢出错误，如果组成部分不能容纳的 32 位数字。

## <a name="examples"></a>示例
下面的表达式返回结果`0.00000090000000000`而无需舍入，因为结果可以适合于`decimal(38,17)`:
```sql
select cast(0.0000009000 as decimal(30,20)) * cast(1.0000000000 as decimal(30,20)) [decimal 38,17]
```
在这种情况下准确度 61，和小数位数为 40。
组成部分 (精度小数位数 = 21) 是小于 32、，因此这种情况 (1) 乘法规则中的，缩放的计算方式为`min(scale, 38 – (precision-scale)) = min(40, 38 – (61-40)) = 17`。 结果类型是`decimal(38,17)`。

下面的表达式返回结果`0.000001`无法放入`decimal(38,6)`:
```sql
select cast(0.0000009000 as decimal(30,10)) * cast(1.0000000000 as decimal(30,10)) [decimal(38, 6)]
```
精度为 61 的这种情况下，小数位数为 20。
刻度大于 6 和整型的一部分 (`precision-scale = 41`) 大于 32。 这种情况 (3) 乘法规则中的，并且结果类型是`decimal(38,6)`。

## <a name="see-also"></a>另请参阅
[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)
  
  

