---
title: 显示大小 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 578bf0cbdf2dd1dbd06dd4a248f4efa5eb839916
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307028"
---
# <a name="display-size"></a>显示大小
列的显示大小是以字符形式显示数据所需的最大字符数。 下表定义了每种 ODBC SQL 数据类型的显示大小。  
  
|SQL 类型标识符|屏幕大小|  
|-------------------------|------------------|  
|所有字符类型[a]|以字符形式显示数据所需的已定义（对于固定类型）或最大（对于变量类型）的字符数。|  
|SQL_DECIMALSQL_NUMERIC|列加 2 的精度（符号、*精度*数字和小数点）。 例如，定义为数字（10，3）的列的显示大小为 12。|  
|SQL_BIT|1（1 位）。|  
|SQL_TINYINT|4，如果签名（一个符号和3位数字）或3，如果无符号（3位）。|  
|SQL_SMALLINT|6，如果签名（一个符号和5位数字）或5，如果无符号（5位）。|  
|SQL_INTEGER|11 如果签名（一个符号和 10 位数字）或 10（未签名（10 位）。|  
|SQL_BIGINT|20（签名时为符号和 19 位数字，如果签名则为 20 位数字（如果未签名）。|  
|SQL_REAL|14（一个符号，7位数字，一个小数点，字母*E，* 一个符号和2位）。|  
|SQL_FLOATSQL_DOUBLE|24（一个符号，15位数字，一个小数点，字母*E，* 一个符号和3位数字）。|  
|所有二进制类型[a]|列的已定义或最大长度（对于变量类型）长度乘以 2。 （每个二进制字节由 2 位十六进制数字表示。|  
|SQL_TYPE_DATE|10 （格式*yyyy-mm-dd*中的日期）。|  
|SQL_TYPE_TIME|8 （格式*hh：mm：sss 的时间*）<br /><br /> - 或 -<br /><br /> 9 = *s（* 格式*hh：mm：ss*[.fff...]的时间，其中*s*是小数秒精度）。|  
|SQL_TYPE_TIMESTAMP|19 （对于*yyyy-mm-dd hh：mm：ss*格式的时间戳）<br /><br /> - 或 -<br /><br /> 20 ° *s* （对于*yyyy-mm-dd hh：mm：ss*[.fff...] 格式的时间戳，其中*s*是小数秒精度）。|  
|所有间隔数据类型|请参阅[间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)。|  
|SQL_GUID|36 *（aaaaaaa-bbbb-cccc-ddd-eeeeeeeeeeeee*格式的字符数|  
  
 [a] 如果驱动程序无法确定变量类型的列或参数长度，则返回SQL_NO_TOTAL。
