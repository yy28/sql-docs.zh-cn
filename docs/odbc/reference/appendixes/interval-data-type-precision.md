---
title: 间隔数据类型精度 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- precision [ODBC]
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: eb73bd77-2e7e-4498-a266-4d7c990a0d56
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44f00ddbbd577731d9485aedc1a63659dfe59414
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="interval-data-type-precision"></a>时间间隔数据类型精度
间隔数据类型的精度包括前导精度、 间隔精度和秒精度的间隔。  
  
 一个时间间隔的前导字段是有符号的数字。 最多的前导字段的位数由调用的数量*间隔前导精度，*这是数据类型声明的部分。 例如，声明： 间隔 HOUR(5) 为分钟具有前导精度为 5; 一个时间间隔小时字段可以采用值从 –99999 至 99999。 描述符记录 SQL_DESC_DATETIME_INTERVAL_PRECISION 字段中包含前导精度的间隔。  
  
 间隔数据类型组成的字段的列表称为*间隔精度*。 它不是数值，术语"精度"可能暗示。 例如，类型间隔天收件人的间隔精度第二个是列表天、 小时、 分钟、 秒。 没有包含此值; 该值的描述符字段始终可以通过间隔数据类型确定时间间隔精度。  
  
 任何具有第二个字段的间隔数据类型具有*秒精度*。 这是允许的秒值的小数部分的十进制数字的数目。 此函数不同于其他数据类型，精度其中表示小数点前的数字个数。 间隔数据类型的秒精度是小数点后的位数。 例如，如果秒精度设置为 6，数字 123456 部分字段中将被解释为.123456 和数量 1230年将被解释为.001230。 对于其他数据类型，这被称为缩放。 间隔秒精度的描述符 SQL_DESC_PRECISION 字段中包含。 如果 SQL 间隔值的小数部分组成的秒部分的精度大于 C 间隔结构中可容纳新增功能，它是驱动程序定义中的 SQL 间隔的秒的小数部分值是否被舍入或截断时转换为 C间隔结构。  
  
 当 SQL_DESC_CONCISE_TYPE 字段设置为间隔的数据类型时，将 SQL_DESC_TYPE 字段设置为 SQL_INTERVAL 和 SQL_DESC_DATETIME_INTERVAL_CODE 设置为间隔数据类型的代码。 SQL_DESC_DATETIME_INTERVAL_PRECISION 字段将自动设置为 2 的默认间隔前导精度和 SQL_DESC_PRECISION 字段将自动设置为 6 的默认间隔秒精度。 如果上述任一值不合适，应用程序应显式设置通过调用描述符字段**SQLSetDescField**。
