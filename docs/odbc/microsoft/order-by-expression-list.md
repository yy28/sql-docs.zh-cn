---
description: ORDER BY 表达式列表
title: ORDER BY 表达式-list |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [ODBC]
- SQL grammar [ODBC], order by clause
ms.assetid: 5ef88186-a99f-4e2c-a3f3-98a42d4f03a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd084a1012d445c89cacba168f21267238bc250f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340613"
---
# <a name="order-by-expression-list"></a>ORDER BY 表达式列表
表达式可以在 ORDER BY 子句中使用。 例如，在以下子句中，表按三个关键表达式排序： a + b、c + d 和 e。  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 不允许对集函数或包含集函数的表达式进行排序。
