---
description: 公历的约束
title: 公历的限制 |Microsoft Docs
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
ms.openlocfilehash: e473c090a889d54de5ca63bd10b07b410936223f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339363"
---
# <a name="constraints-of-the-gregorian-calendar"></a>公历的约束
日期和日期时间数据类型以及间隔数据类型的尾随字段必须符合公历的约束。 这些约束如下：  
  
-   月份字段的值必须介于1和12之间（含这两个值）。  
  
-   Day 字段的值必须介于1到月份中的天数。 月份中的天数由 "年" 和 "月" 字段的值确定，可以是28、29、30或31。  (月中的天数也可能取决于是否为闰年。 )   
  
-   小时字段的值必须介于0和23之间（含0和23）。  
  
-   分钟字段的值必须介于0到59（含）之间。  
  
-   对于间隔数据类型的尾随 seconds 字段，"秒" 字段的值必须介于0到 59.9 (*n*) （含）之间，其中 *n* 为秒的小数部分的位数。  
  
-   对于日期时间数据类型的尾随 seconds 字段，"秒" 字段的值必须介于0到 61.9 (*n*) （含）之间，其中 *n* 指定 "9" 位的数字， *n* 的值为秒的小数部分精度。  (秒范围允许多达两个闰秒，以维持 sidereal 时间的同步。 ) 
