---
title: 数字文本语法 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9daa81e2e0c2e927ee7407d4a00d5d48c333bd54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990709"
---
# <a name="numeric-literal-syntax"></a>数值语法
以下语法用于 ODBC 中的数字文本：  
  
 *numeric-literal* ::= *signed-numeric-literal &#124; unsigned-numeric-literal*  
  
 *signed-numeric-literal* ::= [*sign*] *unsigned-numeric-literal*  
  
 *unsigned-numeric-literal* ::= *exact-numeric-literal &#124; approximate-numeric-literal*  
  
 *exact-numeric-literal* ::= *unsigned-integer* [*period*[*unsigned-integer*]] *&#124;period unsigned-integer*  
  
 *登录*:: =*加号&#124;负号*  
  
 *近似数值文字*:: =*尾数 E 指数*  
  
 *mantissa* ::= *exact-numeric-literal*  
  
 *指数*:: =*已签名整数*  
  
 *已签名整数*:: = [*符号*]*无符号整数*  
  
 *无符号整数*:: =*数字...*  
  
 *plus-sign* ::= *+*  
  
 *minus-sign* ::= -  
  
 *digit* ::= 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *段*:: =。
