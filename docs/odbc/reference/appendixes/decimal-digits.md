---
title: 十进制数字 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- size of data types [ODBC]
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
ms.assetid: 07f3d1fc-b4ee-4693-b342-330b2231b6d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7b9a69941364b32e6b43d79f2d092511fd61f22
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240995"
---
# <a name="decimal-digits"></a>十进制数字
*十进制数字*的 decimal 和 numeric 数据类型指小数点右侧或数据的小数位数的最大位数。 近似的浮点数字列或参数，小数位数是未定义，因为小数点右侧的位数不固定。 对于 datetime 或间隔秒数部分包含的数据，十进制数字被指数据的秒数部分在小数点右侧的位数。  
  
 对于 SQL_DECIMAL 和 SQL_NUMERIC 数据类型，最大的规模通常是最大精度相同。 但是，某些数据源会施加限制最大刻度上。 若要确定数据类型允许的最小值和最大缩放，应用程序调用**SQLGetTypeInfo**。  
  
 下表中显示为每种简洁的 SQL 数据类型定义的十进制数字。  
  
|SQL 类型|十进制数字|  
|--------------|--------------------|  
|所有字符和二进制类型 [a]|不适用|  
|SQL_DECIMAL<br />SQL_NUMERIC|定义的小数点右侧的数字个数。 例如，定义为 NUMERIC(10,3) 列的小数位数为 3。 这可以是负数，而无需使用指数表示法; 支持非常大的数字的存储例如，"12000"可以存储为"12"小数位数为-3。|  
|SQL_DECIMAL 和 SQL_NUMERIC [a] 以外的所有精确数字类型|0|  
|所有近似数据类型 [a]|不适用|  
|SQL_TYPE_DATE，并使用没有秒组件 [a] 的所有间隔类型|不适用|  
|除 SQL_TYPE_DATE，之外的所有日期时间类型和使用秒数部分的所有间隔类型|值 （秒的小数部分） 的秒部分在小数点右侧位数。 此数字不能为负数。|  
|SQL_GUID|不适用|  
  
 [a] *DecimalDigits*的参数**SQLBindParameter**忽略此数据类型。  
  
 为十进制数字返回的值不对应任何一个的描述符字段中的值。 下表中所示，值可以来自于 SQL_DESC_SCALE 或 SQL_DESC_PRECISION 字段，具体取决于数据类型。  
  
|SQL 类型|相对应的描述符字段<br /><br /> 十进制数字|  
|--------------|----------------------------------------------------------|  
|所有字符和二进制类型|不适用|  
|所有的精确数字类型|SCALE|  
|SQL_BIT|不适用|  
|所有近似数值数据类型|不适用|  
|所有日期时间类型|PRECISION|  
|使用秒数部分的所有间隔类型|PRECISION|  
|使用没有秒数部分的所有间隔类型|不适用|
