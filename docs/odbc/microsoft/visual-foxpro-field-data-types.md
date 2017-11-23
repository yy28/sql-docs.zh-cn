---
title: "Visual FoxPro 字段数据类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b4dbb88985b114e0e2f89c4a3f57d8dae4c9210
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 字段数据类型
下表列出的值*FieldType* ALTER TABLE 和 CREATE TABLE 中的自变量，并指示是否*nFieldWidth*和*nPrecision*参数必填。  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Description|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|双精度|  
|C|否|-|宽度的字符字段*n*|  
|D|-|-|日期|  
|F|否|d|浮点数字字段的宽度 *n* 与*d*小数位数|  
|G|-|-|常规|  
|I|-|-|Integer|  
|L|-|-|逻辑函数|  
|M|-|-|备忘录|  
|否|否|d|数值字段的宽度 *n* 与*d*小数位数|  
|T|-|-|DateTime|  
|是|-|-|货币|
