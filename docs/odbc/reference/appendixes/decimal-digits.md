---
title: "十进制数字 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- size of data types [ODBC]
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
ms.assetid: 07f3d1fc-b4ee-4693-b342-330b2231b6d0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4593b1faacfc235ce0ee5c54bc9ca70416444f5e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="decimal-digits"></a>十进制数字
*十进制数字*的 decimal 和 numeric 数据类型定义为最多的到数据的小数位数或小数点右边的位数。 对于近似的浮点数字列或参数，刻度是小数点的未定义的这是小数点的因为不固定右侧的位数。 为日期时间或间隔包含秒数部分的数据，十进制数字被指数据的秒部分在小数点右侧的数字个数。  
  
 对于 SQL_DECIMAL 和 SQL_NUMERIC 数据类型，最多只能缩放通常是相同的最大精度。 但是，某些数据源会施加限制最大刻度上。 若要确定数据类型所允许的最小和最大刻度，应用程序调用**SQLGetTypeInfo**。  
  
 下表中显示为每种简洁的 SQL 数据类型定义的十进制数字。  
  
|SQL 类型|十进制数字|  
|--------------|--------------------|  
|所有字符和二进制类型 [a]|不适用|  
|SQL_DECIMAL<br />SQL_NUMERIC|定义的小数点右侧的数字个数。 例如，定义为 NUMERIC(10,3) 列的小数位数为 3。 这可以是负数，而无需使用指数表示法; 支持的非常大的数字的存储例如，"12000"无法存储为"12"作为增量是小数位数。|  
|SQL_DECIMAL 和 SQL_NUMERIC [a] 以外的所有精确数值类型|0|  
|所有近似数据类型 [a]|不适用|  
|SQL_TYPE_DATE，以及具有没有秒数部分 [a] 的所有间隔类型|不适用|  
|除 SQL_TYPE_DATE，之外的所有日期时间类型以及具有秒数部分的所有间隔类型|值 （秒的小数部分） 的秒部分在小数点右侧的数字个数。 此数字不能为负数。|  
|SQL_GUID|不适用|  
  
 [a] *DecimalDigits*参数**SQLBindParameter**对于此数据类型，将忽略。  
  
 返回用于十进制数字的值不对应中任何一个的描述符字段的值。 值可以来自 SQL_DESC_SCALE 或 SQL_DESC_PRECISION 字段，具体取决于数据类型下, 表中所示。  
  
|SQL 类型|描述符字段对应于<br /><br /> 十进制数字|  
|--------------|----------------------------------------------------------|  
|所有字符和二进制类型|不适用|  
|所有精确数字数据类型|SCALE|  
|SQL_BIT|不适用|  
|所有的近似数值类型|不适用|  
|所有日期时间类型|PRECISION|  
|与秒组件的所有间隔类型|PRECISION|  
|与任何秒组件的所有间隔类型|不适用|

