---
title: 公历的约束 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f67d313f5a1261dba1f88e9ef3a70d30c1cd503
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019186"
---
# <a name="constraints-of-the-gregorian-calendar"></a>公历的约束
日期和日期时间数据类型和 interval 数据类型的尾部字段必须符合公历的约束。 这些约束如下所示：  
  
-   月份字段的值必须介于 1 和 12，非独占。  
  
-   日期字段的值必须介于 1 到月份中的天数。 在每月天数确定年份和月份字段的值和可以为 28、 29、 30 或 31。 （在每月天数可以还依赖于它是否为闰年。）  
  
-   小时字段的值必须介于 0 到 23 之间 （含） 之间。  
  
-   分钟字段的值必须介于 0 和 59 之间 （含） 之间。  
  
-   对于尾随的秒字段值 interval 数据类型，第二个字段的值必须介于 0 和 59.9 (*n*) (含） 之间，其中*n*是秒的小数部分精度的最大位数。  
  
-   对于 datetime 数据类型的尾随秒字段，第二个字段的值必须是介于 0 和 61.9 (*n*) (含） 之间，其中*n*指定的位数"9"和的值*n*秒的小数部分精度。 （秒的范围允许多达两个闰秒以便保持 sidereal 时间同步。）
