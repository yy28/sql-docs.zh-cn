---
title: 间隔数据类型精度 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98be3b4a7e4db30f394a2834364ecab9a20ef182
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706425"
---
# <a name="interval-data-type-precision"></a>间隔数据类型精度
间隔数据类型精度包括间隔起始精度、 时间间隔精度和秒的精度。  
  
 时间间隔的前导字段是有符号的数字。 前导字段的最大位数由名为 quantity*间隔起始精度，* 这是数据类型声明的一部分。 例如，声明： 间隔 HOUR(5) 到分钟具有间隔起始精度为 5;小时字段接受的值从 –99999 至 99999。 间隔起始精度的描述符记录 SQL_DESC_DATETIME_INTERVAL_PRECISION 字段中包含。  
  
 间隔数据类型组成的字段的列表称为*时间间隔精度*。 它不是数值，因为术语"精度"可能暗示。 例如，时间间隔精度类型 INTERVAL DAY TO 的第二个是列表天、 小时、 分钟、 秒。 保存此值; 没有描述符字段时间间隔精度始终可通过间隔数据类型确定。  
  
 任何具有第二个字段的时间间隔数据类型具有*精度的秒数*。 这是值的十进制数字的小数部分的秒中允许的数量。 这是不同于其他数据类型，其中的精度表示小数点前的数字个数。 间隔数据类型的秒精度是小数点后的位数。 例如，如果秒的精度设置为 6，数量 123456 分数字段中将解释为.123456 和号 1230年将解释为.001230。 对于其他数据类型，这被称为规模。 描述符的 SQL_DESC_PRECISION 字段中包含时间间隔的秒精度。 如果 SQL 间隔值的秒小数部分精度大于什么可以保存在 C 间隔结构，它是驱动程序定义中的 SQL 时间间隔的秒的小数部分值是否被舍入或截断时转换为 C间隔结构。  
  
 当 SQL_DESC_CONCISE_TYPE 字段设置为时间间隔数据类型时，SQL_DESC_TYPE 字段设置为 SQL_INTERVAL 和 SQL_DESC_DATETIME_INTERVAL_CODE 设置为时间间隔数据类型的代码。 SQL_DESC_DATETIME_INTERVAL_PRECISION 字段将自动设置为 2 的默认间隔前导精度和 SQL_DESC_PRECISION 字段将自动设置为 6 的默认间隔秒精度。 如果这些值不合适，应用程序应显式设置描述符字段通过调用**SQLSetDescField**。
