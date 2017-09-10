---
title: "按位运算符 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/07/2017
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
- operators [Transact-SQL], bitwise
- bitwise operators
- bit manipulations
ms.assetid: 2b994cf5-2daa-438a-b8c7-4bd8d451ac8d
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: 5d04924a82578040f801864bb68905feebc53e94
ms.contentlocale: zh-cn
ms.lasthandoff: 09/08/2017

---
# <a name="bitwise-operators-transact-sql"></a>位运算符 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  位运算符在两个表达式之间执行位操作，这两个表达式可以为整数数据类型类别中的任何数据类型。  
  按位运算符将两个整数值转换为二进制位，执行 AND、 OR、 或不在每一位，产生的结果的操作。 然后将结果转换为整数。  
  
  例如，整数 170 将转换为二进制 1010 1010年。
将转换为二进制 0100 1011年 75 的整数。

|运算符后的表达式|按位数学|
|---- |---- |
|和 <br> 如果在任何位置的位值均为 1，则结果将是 1。 |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 0000 1010 =  10 |
|或 <br> 如果在任何位置的其中一个位是 1，则结果将是 1。 |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 1110 1011 = 235|
|NOT  <br> 反转位的每个位置处的位值。 |1010 1010 = 170 <br>----------------- <br>  0101 0101 =   85 |
  
请参阅以下主题：   
* [& （位与）](../../t-sql/language-elements/bitwise-and-transact-sql.md)  
* [& = （位与等于）](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
* [&#124;（位或）](../../t-sql/language-elements/bitwise-or-transact-sql.md)  
* [&#124; = （位或等于）](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
* [^ (位异或)](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md)  
* [^ = （位异或等于）](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)  
* [~ （位非）](../../t-sql/language-elements/bitwise-not-transact-sql.md)  
  
 按位运算符的操作数可以是任何一种整数或二进制字符串数据类型类别的数据类型 (除**映像**数据类型)，只不过两个操作数不能为任何一种二进制字符串数据类型数据类型类别。 下表显示所支持的操作数数据类型。  
  
|左操作数|右操作数|  
|------------------|-------------------|  
|[binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**， **smallint**，或**tinyint**|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|**int**， **smallint**， **tinyint**，或**位**|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**， **smallint**， **tinyint**，**二进制**，或**varbinary**|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**， **smallint**， **tinyint**，**二进制**，或**varbinary**|  
|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**， **smallint**， **tinyint**，**二进制**，或**varbinary**|  
|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**， **smallint**，或**tinyint**|  
  
## <a name="see-also"></a>另请参阅  
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
  
  

