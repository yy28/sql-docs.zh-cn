---
title: 在谓词之间 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1f3ff800938574bec81e9cbb86839e014085a2a8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283848"
---
# <a name="between-predicate"></a>BETWEEN 谓词
语法：  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 仅当*表达式1*大于或等于*表达式2*且*表达式1*小于或等于*表达式3*时，才返回 true。  
  
 对于桌面数据库驱动程序和 Microsoft Jet 引擎，此语法的语义是不同的。 在 Microsoft Jet SQL 中，*表达式2*可以大于*表达式3，* 因此仅当*表达式1*大于或等于*表达式3*时，表达式2 才会返回 TRUE，并且*表达式1*小于或等于*表达式2*。
