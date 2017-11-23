---
title: "数值函数 |Microsoft 文档"
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
- functions [ODBC], numeric functions
- numeric functions [ODBC]
ms.assetid: 4fa548dc-e8b0-4179-92ff-81d6a79d10c3
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 861fa1dead42c4bf667b80417c29259f3c3b4aaf
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="numeric-functions"></a>数值函数
下表介绍 ODBC 标量函数集中包含的数值函数。 通过调用**SQLGetInfo**与*信息类型*的 SQL_NUMERIC_FUNCTIONS，应用程序可以确定由驱动程序支持的数值的函数。  
  
 所有数值的函数返回值的数据类型除外 ABS，SQL_FLOAT ROUND、 TRUNCATE、 登录、 FLOOR 和上限，后者返回相同的数据值类型作为输入参数。  
  
 自变量表示为*numeric_exp*可以是列，另一个的标量函数的结果的名称或*数字 litera*l，其中基础数据类型无法表示为 SQL_NUMERIC，SQL_十进制，SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT、 SQL_REAL 或 SQL_DOUBLE。  
  
 自变量表示为*float_exp*可以是列，另一个的标量函数的结果的名称或*数字文本*，其中基础数据类型可以表示为 SQL_FLOAT。  
  
 自变量表示为*integer_exp*可以是列，另一个的标量函数的结果的名称或*数字文本*，其中基础数据类型可以表示为 SQL_TINYINT，SQL_SMALLINT、 SQL_INTEGER 或 SQL_BIGINT。  
  
 已在 ODBC 3.0 为了符合 SQL 92 添加 CURRENT_DATE、 CURRENT_TIME 和 CURRENT_TIMESTAMP 标量函数。  
  
|函数|Description|  
|--------------|-----------------|  
|**ABS (** *numeric_exp* **)** (ODBC 1.0)|返回数值的绝对值*numeric_exp*。|  
|**ACOS (** *float_exp* **)** (ODBC 1.0)|返回的反余弦值*float_exp*作为角度以弧度表示。|  
|**ASIN (** *float_exp* **)** (ODBC 1.0)|返回的反正弦*float_exp*作为角度以弧度表示。|  
|**ATAN (** *float_exp* **)** (ODBC 1.0)|返回的反正切值*float_exp*作为角度以弧度表示。|  
|**ATAN2 (** *float_exp1*， *float_exp2***)** (ODBC 2.0)|返回的反正切值*x*和*y*由指定的坐标*float_exp1*和*float_exp2*分别，角度以弧度为单位表示。|  
|**CEILING (** *numeric_exp* **)** (ODBC 1.0)|返回的最小整数大于或等于*numeric_exp*。 返回值是相同的数据类型作为输入参数。|  
|**COS (** *float_exp* **)** (ODBC 1.0)|返回的余弦值*float_exp*，其中*float_exp*是以弧度表示的角度。|  
|**COT (** *float_exp* **)** (ODBC 1.0)|返回的余切值*float_exp*，其中*float_exp*是以弧度表示的角度。|  
|**度 (** *numeric_exp* **)** (ODBC 2.0)|返回的度数转换从*numeric_exp*弧度为单位。|  
|**EXP (** *float_exp* **)** (ODBC 1.0)|返回的指数值*float_exp*。|  
|**FLOOR (** *numeric_exp* **)** (ODBC 1.0)|返回小于或等于最大整数*numeric_exp*。 返回值是相同的数据类型作为输入参数。|  
|**日志 (** *float_exp* **)** (ODBC 1.0)|返回的自然对数*float_exp*。|  
|**LOG10 (** *float_exp* **)** (ODBC 2.0)|返回基 10 对数*float_exp*。|  
|**MOD (** *integer_exp1*， *integer_exp2***)** (ODBC 1.0)|返回的其余部分 （取模） *integer_exp1*除以*integer_exp2*。|  
|**PI （)** (ODBC 1.0)|浮点值形式返回 pi 的常量值。|  
|**电源 (** *numeric_exp*， *integer_exp***)** (ODBC 2.0)|返回的值*numeric_exp*的次幂*integer_exp*。|  
|**弧度 (** *numeric_exp* **)** (ODBC 2.0)|返回从转换的弧度数*numeric_exp*度。|  
|**RAND (**[*integer_exp*]**)** (ODBC 1.0)|返回随机浮点值使用*integer_exp*作为可选种子值。|  
|**ROUND (** *numeric_exp*， *integer_exp***)** (ODBC 2.0)|返回*numeric_exp*舍入为*integer_exp*放置小数点右侧。 如果*integer_exp*为负， *numeric_exp*舍入为 &#124;*integer_exp*&#124; 小数点左侧的位数。|  
|**登录 (** *numeric_exp* **)** (ODBC 1.0)|返回的符号的指示符*numeric_exp*。 如果*numeric_exp*为小于零个、 1 返回。 如果*numeric_exp*等于零，则返回 0。 如果*numeric_exp*大于零，则返回 1。|  
|**SIN (** *float_exp* **)** (ODBC 1.0)|返回的正弦值*float_exp*，其中*float_exp*是以弧度表示的角度。|  
|**SQRT (** *float_exp* **)** (ODBC 1.0)|返回的平方根*float_exp*。|  
|**TAN (** *float_exp* **)** (ODBC 1.0)|返回的正切值*float_exp*，其中*float_exp*是以弧度表示的角度。|  
|**截断 (** *numeric_exp*， *integer_exp***)** (ODBC 2.0)|返回*numeric_exp*截断为*integer_exp*放置小数点右侧。 如果*integer_exp*为负， *numeric_exp*截断为 &#124;*integer_exp*&#124; 小数点左侧的位数。|
