---
title: 数字函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], numeric functions
- numeric functions [ODBC]
ms.assetid: 4fa548dc-e8b0-4179-92ff-81d6a79d10c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 03da5b6644e0f7df3dc4e5e16a211cb503023bad
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299867"
---
# <a name="numeric-functions"></a>数值函数
下表描述了 ODBC 标量函数集中包含的数字函数。 通过使用SQL_NUMERIC_FUNCTIONS*的信息类型*调用**SQLGetInfo，** 应用程序可以确定驱动程序支持哪些数值函数。  
  
 除 ABS、ROUND、TRUNCATE、SIGN、FLOOR 和"天花板"之外，所有数值函数都返回数据类型的值SQL_FLOAT，这些值返回与输入参数相同的数据类型的值。  
  
 表示为*numeric_exp*的参数可以是列的名称、另一个标量函数的结果或*数字-litera*l，其中基础数据类型可以表示为SQL_NUMERIC、SQL_DECIMAL、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_FLOAT、SQL_REAL或SQL_DOUBLE。  
  
 表示为*float_exp*的参数可以是列的名称、另一个标量函数的结果或*数字文本*，其中基础数据类型可以表示为SQL_FLOAT。  
  
 表示为*integer_exp*的参数可以是列的名称、另一个标量函数的结果或*数字文本*，其中基础数据类型可以表示为SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER或SQL_BIGINT。  
  
 在 ODBC 3.0 中添加了CURRENT_DATE、CURRENT_TIME和CURRENT_TIMESTAMP标量函数，以便与 SQL-92 对齐。  
  
|函数|说明|  
|--------------|-----------------|  
|**ABS（numeric_exp** _numeric_exp_ **）** （ODBC 1.0）|返回*numeric_exp*的绝对值 。|  
|**ACOS（** _float_exp_ **）** （ODBC 1.0）|返回*float_exp*的弧形作为角度，以弧度表示。|  
|**阿辛（float_exp** _float_exp_ **）** （ODBC 1.0）|返回*float_exp*的弧线作为角度，以弧度表示。|  
|**阿坦 （float_exp** _float_exp_ **）** （ODBC 1.0）|返回*float_exp*的弧形作为角度，以弧度表示。|  
|**ATAN2（float_exp1，float_exp2）** _float_exp1_（ODBC 2.0） _float_exp2_**)**|返回*x*和*y*坐标的弧形，分别由*float_exp1*和*float_exp2*指定，作为角度，以弧度表示。|  
|**天花板（numeric_exp** _numeric_exp_ **）** （ODBC 1.0）|返回大于或等于*numeric_exp*的最小整数。 返回值与输入参数的数据类型相同。|  
|**COS（** _float_exp_ **）** （ODBC 1.0）|返回*float_exp*的可成因，其中*float_exp*是以弧度表示的角度。|  
|**COT（** _float_exp_ **）** （ODBC 1.0）|返回*float_exp*的共量，其中*float_exp*是以弧度表示的角度。|  
|**学位（numeric_exp** _numeric_exp_ **）** （ODBC 2.0）|返回从*numeric_exp*弧度转换的度数。|  
|**EXP（** _float_exp_ **）** （ODBC 1.0）|返回*float_exp*的指数值。|  
|**地板（numeric_exp** _numeric_exp_ **）** （ODBC 1.0）|返回小于或等于*numeric_exp*的最大整数。 返回值与输入参数的数据类型相同。|  
|**日志（float_exp** _float_exp_ **）** （ODBC 1.0）|返回*float_exp*的自然对数。|  
|**日志10（float_exp** _float_exp_ **）** （ODBC 2.0）|返回*float_exp*的基 10 对数。|  
|**MOD（integer_exp1，integer_exp2** _integer_exp1_ _integer_exp2_**）** （ODBC 1.0）|返回*integer_exp1*的剩余数（模数）除以*integer_exp2*。|  
|**PI（** （ODBC 1.0）|将 pi 的常量值作为浮点值返回。|  
|**电源（numeric_exp** _numeric_exp_ _，integer_exp_**）** （ODBC 2.0）|将*numeric_exp*的值返回到*integer_exp*的功率。|  
|**拉迪安斯（** _numeric_exp_ **）** （ODBC 2.0）|返回从*numeric_exp*度转换的弧度数。|  
|**兰德 （**[*integer_exp*+**）** （ODBC 1.0）|使用*integer_exp*作为可选种子值返回随机浮点值。|  
|**圆 （numeric_exp** _numeric_exp_， _integer_exp_**）** （ODBC 2.0）|*返回numeric_exp*舍入到小数点右侧*integer_exp*位。 如果*integer_exp*为负数，*则numeric_exp*将四舍五入到 *&#124;integer_exp*小数点左侧的&#124;位。|  
|**标志（numeric_exp** _numeric_exp_ **）（ODBC** 1.0）|返回*numeric_exp*标志的指示器。 如果*numeric_exp*小于零，则返回 -1。 如果*numeric_exp*等于零，则返回 0。 如果*numeric_exp*大于零，则返回 1。|  
|**SIN（** _float_exp_ **）** （ODBC 1.0）|返回*float_exp*的正则，其中*float_exp*是以弧度表示的角度。|  
|**SQRT（** _float_exp_ **）** （ODBC 1.0）|返回*float_exp*的平方根。|  
|**褐色（float_exp** _float_exp_ **）** （ODBC 1.0）|返回*float_exp*的切线，其中*float_exp*是以弧度表示的角度。|  
|**（numeric_exp，** _numeric_exp_integer_exp _integer_exp_**）** （ODBC 2.0）|*返回numeric_exp*截断到小数点右侧*integer_exp*位。 如果*integer_exp*为负数，*则numeric_exp*将被截断为&#124;*integer_exp*小数点左侧的&#124;位。|
