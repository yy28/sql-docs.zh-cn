---
title: 谓词之间 |Microsoft 文档
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
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 538d1a6600d0b47967ad7ed67d9a07843af15c29
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="between-predicate"></a>谓词之间
语法：  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 返回 true 才*expression1*大于或等于*expression2*和*expression1*小于或等于*expression3*.  
  
 此语法的语义是不同的桌面数据库驱动程序和 Microsoft Jet 引擎。 在 Microsoft Jet SQL *expression2*可以大于*expression3* ，以便该语句将返回 TRUE，仅当*expression1*大于或等于*expression3*，和*expression1*小于或等于*expression2*。
