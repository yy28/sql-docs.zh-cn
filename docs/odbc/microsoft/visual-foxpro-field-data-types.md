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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 217058bf328677bf375d346ae7201c6eb81efa4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087942"
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 字段数据类型
下表列出了 ALTER TABLE 和 CREATE TABLE 中的*FieldType*参数的值，并指示是否需要*nFieldWidth*和*nPrecision*参数。  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|说明|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|宽度为*n*的字符字段|  
|D|-|-|Date|  
|F|N|d|宽度为*n*且带有*d*个小数点的浮动数值字段|  
|G|-|-|常规|  
|I|-|-|Integer|  
|L|-|-|逻辑|  
|M|-|-|备忘录|  
|N|N|d|宽度为*n*且带有*d*小数位的数值字段|  
|T|-|-|DateTime|  
|Y|-|-|货币|
