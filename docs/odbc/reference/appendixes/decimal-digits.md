---
title: 十进制数字 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4921a6162b6d711e657f223b5be5783dfa37bca8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285157"
---
# <a name="decimal-digits"></a>十进制数字
十进制和数字数据类型*的小数位数*定义为小数点右侧的最大位数或数据的比例。 对于近似的浮点数列或参数，比例未定义，因为小数点右侧的数字数不是固定的。 对于包含秒分量的日期时间或间隔数据，十进制数字定义为数据秒组件中小数点右侧的数字数。  
  
 对于SQL_DECIMAL和SQL_NUMERIC数据类型，最大比例通常与最大精度相同。 但是，某些数据源对最大比例施加了单独的限制。 要确定数据类型允许的最小和最大比例，应用程序调用**SQLGetTypeInfo**。  
  
 为每种简洁的 SQL 数据类型定义的小数位数显示在下表中。  
  
|SQL 类型|十进制数字|  
|--------------|--------------------|  
|所有字符和二进制类型[a]|不适用|  
|SQL_DECIMAL<br />SQL_NUMERIC|小数点右侧的已定义数字数。 例如，定义为数字（10，3）的列比例为 3。 这可以是负数，以支持存储非常大的数字，而无需使用指数表示法;例如，"12000"可以存储为"12"，其比例为-3。|  
|SQL_DECIMAL和SQL_NUMERIC以外的所有精确数值类型|0|  
|所有近似数据类型[a]|不适用|  
|SQL_TYPE_DATE，并且所有间隔类型，没有秒分量 [a]|不适用|  
|除SQL_TYPE_DATE之外的所有日期时间类型以及具有秒组件的所有间隔类型|值的秒部分（分数秒）中小数点右侧的数字数。 此数字不能为负数。|  
|SQL_GUID|不适用|  
  
 [a] 此数据类型将忽略**SQLBind 参数**的*十进制参数*。  
  
 为小数位数返回的值与任何一个描述符字段中的值不对应。 这些值可以来自SQL_DESC_SCALE或SQL_DESC_PRECISION字段，具体取决于数据类型，如下表所示。  
  
|SQL 类型|与<br /><br /> 十进制数字|  
|--------------|----------------------------------------------------------|  
|所有字符和二进制类型|不适用|  
|所有确切的数值类型|SCALE|  
|SQL_BIT|不适用|  
|所有近似数值类型|不适用|  
|所有日期时间类型|PRECISION|  
|具有秒组件的所有间隔类型|PRECISION|  
|所有间隔类型，无秒分量|不适用|
