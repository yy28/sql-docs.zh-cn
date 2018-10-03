---
title: 数值函数 （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC numeric functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], numeric functions
- numeric functions [ODBC]
- FoxPro ODBC driver [ODBC], numeric functions
ms.assetid: 7caab48e-cbb5-4bbc-a09b-5cf902e5bc45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73379b769da61fe14ba18815446337d0172c2805
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654390"
---
# <a name="numeric-functions-visual-foxpro-odbc-driver"></a>数字函数（Visual FoxPro ODBC 驱动程序）
下表描述了支持的 Visual FoxPro ODBC 驱动程序; ODBC 数值函数在相同的功能的 Visual FoxPro 语法与 ODBC 语法不同，会列出等效 Visual FoxPro。  
  
|ODBC 语法|Visual FoxPro 语法|  
|------------------|---------------------------|  
|ABS *(则 numeric_exp)*||  
|ACOS *(float_exp)*||  
|ASIN *(float_exp)*||  
|ATAN *(float_exp)*||  
|ATAN2 *(float_exp1，float_exp2)*|ATN2 (*float_exp1，float_exp2*)|  
|CEILING *(则 numeric_exp)*||  
|COS *(float_exp)*||  
|COT *(float_exp)*||  
|度 *(则 numeric_exp)*|RTOD *(则 numeric_exp)*|  
|EXP *(float_exp)*||  
|FLOOR *(则 numeric_exp)*||  
|日志 *(float_exp)*||  
|LOG10 *(float_exp)*||  
|MOD *(integer_exp1，integer_exp2)*||  
|PI *（)*||  
|弧度 *(则 numeric_exp)*|DTOR *(则 numeric_exp)*|  
|RAND *([integer_exp])*||  
|ROUND *(则 numeric_exp，integer_exp)*||  
|登录 *(则 numeric_exp)*||  
|SIN *(float_exp)*||  
|SQRT *(float_exp)*||  
|TAN *(float_exp)*||  
  
 不支持以下数值函数：  
  
 POWER *(则 numeric_exp，integer_exp)*  
  
 截断 *(则 numeric_exp，integer_exp)*
