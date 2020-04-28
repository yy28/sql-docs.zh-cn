---
title: Visual FoxPro 字段数据类型 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304798"
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 字段数据类型
下表列出了 ALTER TABLE 和 CREATE TABLE 中的*FieldType*参数的值，并指示是否需要*nFieldWidth*和*nPrecision*参数。  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|说明|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|宽度为*n*的字符字段|  
|D|-|-|日期|  
|F|N|d|宽度为*n*且带有*d*个小数点的浮动数值字段|  
|G|-|-|常规|  
|I|-|-|Integer|  
|L|-|-|逻辑|  
|M|-|-|备忘录|  
|N|N|d|宽度为*n*且带有*d*小数位的数值字段|  
|T|-|-|DateTime|  
|Y|-|-|货币|
