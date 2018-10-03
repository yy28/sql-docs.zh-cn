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
manager: craigg
ms.openlocfilehash: 07aa06eae9f1e75a047bdd302754d884790436e1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806109"
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 字段数据类型
下表列出了值*FieldType* ALTER TABLE 和 CREATE TABLE 中的参数，并指示是否*nFieldWidth*并*nPrecision*参数必填。  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Description|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|双精度|  
|C|N|-|字符宽度的字段*n*|  
|D|-|-|date|  
|F|N|d|浮点数值字段的宽度*n*与*d*小数位数|  
|G|-|-|常规|  
|I|-|-|Integer|  
|L|-|-|逻辑函数|  
|M|-|-|备忘录|  
|N|N|d|数值字段的宽度*n*与*d*小数位数|  
|T|-|-|DateTime|  
|Y|-|-|货币|
