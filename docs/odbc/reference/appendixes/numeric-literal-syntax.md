---
title: "数字文本语法 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a371ac49fe29674a1e9c0d7bb0dd9639ba5aa48
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="numeric-literal-syntax"></a>数字文本语法
以下语法用于 ODBC 中的数字文本：  
  
 *数字文本*:: =*签名数字文本 &#124; 无符号数值文本*  
  
 *签名数字文本*:: = [*登录*]*无符号数值文本*  
  
 *无符号数值文本*:: =*精确数值文本 &#124; 近似数值文本*  
  
 *精确数字文本*:: =*无符号整数*[*段*[*无符号整数*]] *&#124; 期间无符号整数*  
  
 *登录*:: =*加号 &#124; 负号*  
  
 *近似数值文本*:: =*尾数 E 的指数*  
  
 *尾数*:: =*精确数值文本*  
  
 *指数*:: =*有符号整数*  
  
 *有符号整数*:: = [*登录*]*无符号整数*  
  
 *无符号整数*:: =*数字...*  
  
 *加号*:: =*+*  
  
 *负号*:: =-  
  
 *数字*:: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *段*:: =。
