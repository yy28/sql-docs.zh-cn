---
title: 可视化 FoxPro 字段数据类型 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 72313e0269c93bca9cb2561d89604c3c88c8567b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304798"
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 字段数据类型
下表列出了 ALTER TABLE 和 CREATE TABLE 中*字段类型*参数的值，并指示是否需要*nFieldWidth*和*nPrecision*参数。  
  
|*字段类型*|*NFieldWidth*|*n精密*|描述|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|*宽度*n 的字符字段|  
|D|-|-|Date|  
|F|N|d|具有*d*小数位点的宽度*n*的浮动数字字段|  
|G|-|-|常规|  
|I|-|-|Integer|  
|L|-|-|逻辑|  
|M|-|-|备忘录|  
|N|N|d|带有*d*小数位的数字宽度*字段 n*|  
|T|-|-|DateTime|  
|Y|-|-|货币|
