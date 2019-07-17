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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1a0ac99729966acdcb03c2aab0175c34bba0c08a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138118"
---
# <a name="between-predicate"></a>BETWEEN 谓词
语法：  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 返回 true 才*expression1*大于或等于*expression2*并*expression1*小于或等于*expression3*.  
  
 此语法的语义是不同的桌面数据库驱动程序和 Microsoft Jet 引擎。 在 Microsoft Jet SQL *expression2*可能会超出*expression3* ，以便该语句将返回 TRUE，仅当*expression1*大于或等于*expression3*，并*expression1*小于或等于*expression2*。
