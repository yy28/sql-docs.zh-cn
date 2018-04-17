---
title: Visual FoxPro 字段数据类型 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ccb1adbe822aeb29bd34749333d59b6b67f6f5fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 字段数据类型
下表列出的值*FieldType* ALTER TABLE 和 CREATE TABLE 中的自变量，并指示是否*nFieldWidth*和*nPrecision*参数必填。  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Description|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|双精度|  
|C|否|-|宽度的字符字段*n*|  
|D|-|-|日期|  
|F|否|d|浮点数字字段的宽度*n*与*d*小数位数|  
|G|-|-|常规|  
|I|-|-|Integer|  
|L|-|-|逻辑函数|  
|M|-|-|备忘录|  
|否|否|d|数值字段的宽度*n*与*d*小数位数|  
|T|-|-|DateTime|  
|是|-|-|货币|
