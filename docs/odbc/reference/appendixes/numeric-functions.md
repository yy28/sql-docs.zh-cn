---
title: 数值函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e744d3de177197923540fc3101c58dcbb4d3490
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990727"
---
# <a name="numeric-functions"></a>数值函数
下表介绍 ODBC 标量函数集中包含的数值函数。 通过调用**SQLGetInfo**与*信息类型*的 SQL_NUMERIC_FUNCTIONS，应用程序可以确定由驱动程序支持的数值的函数。  
  
 所有数值函数的返回值数据类型除外 ABS，SQL_FLOAT ROUND、 TRUNCATE、 登录、 FLOOR、 和上限，后者返回值相同的数据类型作为输入参数。  
  
 参数表示为*则 numeric_exp*可以是列，另一个标量函数的结果的名称或*数字 litera*l，其中的基础数据类型可以表示为 SQL_NUMERIC，SQL_DECIMAL、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT、 SQL_REAL 或 SQL_DOUBLE。  
  
 参数表示为*float_exp*可以是列，另一个标量函数的结果的名称或*数值文字*，可在其中显示基础数据类型作为 SQL_FLOAT。  
  
 参数表示为*integer_exp*可以是列，另一个标量函数的结果的名称或*数值文字*，其中的基础数据类型可以表示为 SQL_TINYINT，SQL_SMALLINT、 SQL_INTEGER 或 SQL_BIGINT。  
  
 ODBC 3.0 以符合 SQL-92 中添加了 CURRENT_DATE、 CURRENT_TIME 和 CURRENT_TIMESTAMP 标量函数。  
  
|函数|描述|  
|--------------|-----------------|  
|**ABS(** _numeric_exp_ **)**  (ODBC 1.0)|返回的绝对值*则 numeric_exp*。|  
|**ACOS(** _float_exp_ **)**  (ODBC 1.0)|返回的反余弦*float_exp*作为角度以弧度表示。|  
|**ASIN(** _float_exp_ **)**  (ODBC 1.0)|返回的反正弦*float_exp*作为角度以弧度表示。|  
|**ATAN(** _float_exp_ **)**  (ODBC 1.0)|返回的反正切*float_exp*作为角度以弧度表示。|  
|**ATAN2(** _float_exp1_, _float_exp2_ **)**  (ODBC 2.0)|返回的反正切值*x*并*y*指定的坐标*float_exp1*并*float_exp2*，分别为角度，以弧度为单位表示。|  
|**CEILING(** _numeric_exp_ **)**  (ODBC 1.0)|返回的最小整数大于或等于*则 numeric_exp*。 返回值是相同的数据类型作为输入参数。|  
|**COS(** _float_exp_ **)**  (ODBC 1.0)|返回的余弦*float_exp*，其中*float_exp*是以弧度为单位表示的角。|  
|**COT(** _float_exp_ **)**  (ODBC 1.0)|返回的余切*float_exp*，其中*float_exp*是以弧度为单位表示的角。|  
|**DEGREES(** _numeric_exp_ **)**  (ODBC 2.0)|返回从转换为度数*则 numeric_exp*弧度为单位。|  
|**EXP(** _float_exp_ **)**  (ODBC 1.0)|返回的指数值*float_exp*。|  
|**FLOOR(** _numeric_exp_ **)**  (ODBC 1.0)|返回小于或等于最大整数*则 numeric_exp*。 返回值是相同的数据类型作为输入参数。|  
|**LOG(** _float_exp_ **)**  (ODBC 1.0)|返回自然对数*float_exp*。|  
|**LOG10(** _float_exp_ **)**  (ODBC 2.0)|返回基数为 10 的对数*float_exp*。|  
|**MOD(** _integer_exp1_, _integer_exp2_ **)**  (ODBC 1.0)|返回余数 （取模） *integer_exp1*除以*integer_exp2*。|  
|**PI （)** (ODBC 1.0)|浮点值形式返回 pi 的常量值。|  
|**POWER(** _numeric_exp_, _integer_exp_ **)**  (ODBC 2.0)|返回的值*则 numeric_exp*的幂*integer_exp*。|  
|**RADIANS(** _numeric_exp_ **)**  (ODBC 2.0)|返回从转换为弧度数*则 numeric_exp*度。|  
|**RAND(** [*integer_exp*] **)**  (ODBC 1.0)|返回随机浮点值使用*integer_exp*作为可选的种子值。|  
|**ROUND (** _则 numeric_exp_， _integer_exp_ **)** (ODBC 2.0)|返回*则 numeric_exp*舍入到*integer_exp*放置的小数点右侧。 如果*integer_exp*为负，*则 numeric_exp*舍入到&#124; *integer_exp* &#124;将放置到小数点左侧。|  
|**SIGN(** _numeric_exp_ **)**  (ODBC 1.0)|返回的符号的指示器*则 numeric_exp*。 如果*则 numeric_exp*小于零，-1 返回。 如果*则 numeric_exp*等于零，则返回 0。 如果*则 numeric_exp*是大于零，则返回 1。|  
|**SIN(** _float_exp_ **)**  (ODBC 1.0)|返回的正弦*float_exp*，其中*float_exp*是以弧度为单位表示的角。|  
|**SQRT(** _float_exp_ **)**  (ODBC 1.0)|返回的平方根*float_exp*。|  
|**TAN(** _float_exp_ **)**  (ODBC 1.0)|返回的正切*float_exp*，其中*float_exp*是以弧度为单位表示的角。|  
|**TRUNCATE(** _numeric_exp_, _integer_exp_ **)**  (ODBC 2.0)|返回*则 numeric_exp*被截尾取*integer_exp*放置的小数点右侧。 如果*integer_exp*为负，*则 numeric_exp*将被截断为&#124; *integer_exp* &#124;将放置到小数点左侧。|
