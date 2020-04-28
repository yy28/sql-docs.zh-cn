---
title: BETWEEN 谓词 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283848"
---
# <a name="between-predicate"></a>BETWEEN 谓词
语法：  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 仅当*表达式*2 大于或等于*表达式*2 且*表达式*2 小于或等于*expression3*时，才返回 true。  
  
 对于桌面数据库驱动程序和 Microsoft Jet 引擎，此语法的语义不同。 在 Microsoft Jet SQL 中，*表达式*2 可以大于*expression3* ，因此，仅当*表达式表达式*大于或等于*expression3*，*表达式*2 小于或等于*表达式*2 时，该语句才返回 TRUE。
