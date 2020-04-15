---
title: 公历的约束 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Gregorian calendar
- Gregorian calendar [ODBC]
ms.assetid: 70667410-c582-4369-8e06-9d98e21cd2bf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f88842c7426e17af1fdc0533b8b97e2c559de237
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284757"
---
# <a name="constraints-of-the-gregorian-calendar"></a>公历的约束
日期和日期时间数据类型以及间隔数据类型的尾随字段必须符合公历的约束。 这些限制如下：  
  
-   月字段的值必须介于 1 和 12 之间（包括）。  
  
-   日字段的值必须在 1 到月份天数的范围内。 当月中的天数根据年份和月份字段的值确定，可以为 28、29、30 或 31。 （当月中的天数还取决于它是否是闰年。  
  
-   小时字段的值必须介于 0 和 23 之间（包括）。  
  
-   分钟字段的值必须介于 0 和 59 之间（包括）。  
  
-   对于间隔数据类型的尾随秒字段，秒字段的值必须介于 0 和 59.9（n ）*n*之间，其中*n*是小数秒精度中的位数。  
  
-   对于日期时间数据类型的尾随秒字段，秒字段的值必须介于 0 和 61.9（n ）*n*之间，其中*n*指定"9"位数 *，n*的值为小数秒精度。 （秒的范围允许多达两个闰秒来保持次真时间的同步。
