---
description: 数字函数（Visual FoxPro ODBC 驱动程序）
title: " (Visual FoxPro ODBC 驱动程序) 的数值函数 |Microsoft Docs"
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c8728446decd8a0ad04f08d88475ae08a7c69c5f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449369"
---
# <a name="numeric-functions-visual-foxpro-odbc-driver"></a>数字函数（Visual FoxPro ODBC 驱动程序）
下表描述了 Visual FoxPro ODBC 驱动程序支持的 ODBC 数字函数;当同一个函数的 Visual FoxPro 语法与 ODBC 语法不同时，将列出等效的 Visual FoxPro。  
  
|ODBC 语法|Visual FoxPro 语法|  
|------------------|---------------------------|  
|ABS * (numeric_exp) *||  
|ACOS * (float_exp) *||  
|ASIN * (float_exp) *||  
|ATAN * (float_exp) *||  
|ATAN2 * (float_exp1，float_exp2) *|ATN2 (*float_exp1，float_exp2*) |  
|天花板 * (numeric_exp) *||  
|COS * (float_exp) *||  
|COT * (float_exp) *||  
|度数 * (numeric_exp) *|RTOD * (numeric_exp) *|  
|EXP * (float_exp) *||  
|楼层 * (numeric_exp) *||  
|日志 * (float_exp) *||  
|LOG10 * (float_exp) *||  
|MOD * (integer_exp1，integer_exp2) *||  
|PI * ( ) *||  
|RADIANS * (numeric_exp) *|DTOR * (numeric_exp) *|  
|RAND * ( [integer_exp] ) *||  
|舍入 * (numeric_exp，integer_exp) *||  
|签名 * (numeric_exp) *||  
|SIN * (float_exp) *||  
|SQRT * (float_exp) *||  
|茶色 * (float_exp) *||  
  
 不支持以下数值函数：  
  
 POWER * (numeric_exp，integer_exp) *  
  
 截断 * (numeric_exp，integer_exp) *
