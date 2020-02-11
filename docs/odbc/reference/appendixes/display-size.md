---
title: 显示大小 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 61afd5c9932f58c49e54b4aff8b053d0a25a6e3f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68130022"
---
# <a name="display-size"></a>显示大小
列的显示大小是以字符形式显示数据所需的最大字符数。 下表定义了每个 ODBC SQL 数据类型的显示大小。  
  
|SQL 类型标识符|显示大小|  
|-------------------------|------------------|  
|所有字符类型 [a]|定义的（用于固定类型）或最大值（对于变量类型），以字符形式显示数据所需的字符数。|  
|SQL_DECIMAL SQL_NUMERIC|列的精度加2（符号、*精度*数字和小数点）。 例如，定义为数值（10，3）的列的显示大小为12。|  
|SQL_BIT|1（1位数）。|  
|SQL_TINYINT|如果符号为（符号和3位），则为 4; 如果无符号（3位数），则为3。|  
|SQL_SMALLINT|如果签名（符号和5位数字），则为 6; 如果未签名（5位数字），则为5。|  
|SQL_INTEGER|11如果有符号（符号和10位数字）或10（如果无符号，则为10个数字）。|  
|SQL_BIGINT|20（符号和19位数字，如果有符号，则为20位）。|  
|SQL_REAL|14（符号、7位数、小数点、字母*E*、正负号和2位数字）。|  
|SQL_FLOAT SQL_DOUBLE|24（符号、15位数、小数点、字母*E*、正负号和3位数字）。|  
|所有二进制类型 [a]|列乘2的定义的或最大值（对于变量类型）。 （每个二进制字节由2位十六进制数字表示。）|  
|SQL_TYPE_DATE|10（格式为*yyyy-mm-dd*的日期）。|  
|SQL_TYPE_TIME|8（格式为*hh： mm： ss*）<br /><br /> - 或 -<br /><br /> 9 + *s* （格式为*hh： mm： ss*[. fff ...]，其中*s*为秒的小数部分精度）。|  
|SQL_TYPE_TIMESTAMP|19（对于*yyyy-mm-dd hh： mm： ss*格式的时间戳）<br /><br /> - 或 -<br /><br /> 20 +*秒*（对于*yyyy-mm-dd hh： mm： ss*[. fff ...] 格式的时间戳，其中*s*为秒的小数部分精度）。|  
|所有间隔数据类型|请参阅[间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)。|  
|SQL_GUID|36（ *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*格式的字符数|  
  
 [a] 如果驱动程序无法确定变量类型的列或参数长度，它将返回 SQL_NO_TOTAL。
