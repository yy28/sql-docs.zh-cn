---
title: 间隔数据类型精度 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 746293c545c47917abd084ec3eb105051fc2fbcf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290737"
---
# <a name="interval-data-type-precision"></a>间隔数据类型精度
间隔数据类型的精度包括间隔前导精度、间隔精度和秒精度。  
  
 间隔的领先字段是已签名的数字。 前导字段的最大位数由称为*间隔前导精度*的数量确定，该量是数据类型声明的一部分。 例如，声明：INTERVAL HOUR（5）到分钟的间隔前置精度为5;HOUR 字段可以获取 -99999 到 99999 的值。 间隔前导精度包含在描述符记录的SQL_DESC_DATETIME_INTERVAL_PRECISION字段中。  
  
 间隔数据类型组成的字段列表称为*间隔精度*。 它不是数值，因为术语"精度"可能暗示。 例如，"间隔日到秒"类型的间隔精度是列表天、小时、分钟、秒。 没有包含此值的描述符字段;因此，没有描述符字段。间隔精度始终可以通过间隔数据类型确定。  
  
 具有"秒"字段的任何间隔数据类型都有*秒精度*。 这是秒值小数部分允许的小数位数。 这与其他数据类型不同，其中精度指示小数点之前的数字数。 间隔数据类型的秒精度是小数点之后的位数。 例如，如果秒精度设置为 6，则分数字段中的数字 123456 将解释为 .123456，数字 1230 将解释为 .001230。 对于其他数据类型，这称为缩放。 间隔秒精度包含在描述符的SQL_DESC_PRECISION字段中。 如果 SQL 间隔值的小数秒分量的精度大于 C 间隔结构中可以保留的精度，则驱动程序定义 SQL 间隔中的小数秒值在转换为 C 间隔结构时是四舍五入还是截断。  
  
 当SQL_DESC_CONCISE_TYPE字段设置为间隔数据类型时，SQL_DESC_TYPE字段设置为SQL_INTERVAL，SQL_DESC_DATETIME_INTERVAL_CODE设置为间隔数据类型的代码。 SQL_DESC_DATETIME_INTERVAL_PRECISION字段将自动设置为默认间隔前导精度为 2，SQL_DESC_PRECISION字段将自动设置为默认间隔秒精度为 6。 如果其中任一值不合适，则应用程序应通过调用**SQLSetDescField**显式设置描述符字段。
