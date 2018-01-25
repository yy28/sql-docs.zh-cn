---
title: "按位运算符 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- operators [Transact-SQL], bitwise
- bitwise operators
- bit manipulations
ms.assetid: 2b994cf5-2daa-438a-b8c7-4bd8d451ac8d
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: b0706080c0a878987fab8d2cc5f0c1677f43309b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="bitwise-operators-transact-sql"></a>位运算符 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
* [& &#40;按位 AND &#41;](../../t-sql/language-elements/bitwise-and-transact-sql.md)  
* [& = &#40;按位与赋值 &#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
* [&#124;&#40;按位 OR 运算符 &#41;](../../t-sql/language-elements/bitwise-or-transact-sql.md)  
* [&#124; = &#40;按位 OR 赋值 &#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
* [^ &#40;按位异或 &#41;](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md)  
* [^ = &#40;按位异或赋值 &#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)  
* [~ &#40;位非 &#41;](../../t-sql/language-elements/bitwise-not-transact-sql.md)  
  
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
 [复合运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
  
