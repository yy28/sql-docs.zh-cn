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
manager: craigg
ms.openlocfilehash: 18b1c144e84bf0be5aaeb68b66660f7bc7865ade
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601535"
---
# <a name="numeric-literal-syntax"></a>数值语法
以下语法用于 ODBC 中的数字文本：  
  
 *数值文字*:: =*签名数字文本&#124;无符号数字文本*  
  
 *签名数值文字*:: = [*符号*]*无符号数字文本*  
  
 *无符号数值文字*:: =*精确数字文本&#124;近似数字文本*  
  
 *精确数值文字*:: =*无符号整数*[*段*[*无符号整数*]] *&#124;时间段的无符号整数*  
  
 *登录*:: =*加号&#124;负号*  
  
 *近似数值文字*:: =*尾数 E 指数*  
  
 *尾数*:: =*精确数字文本*  
  
 *指数*:: =*已签名整数*  
  
 *已签名整数*:: = [*符号*]*无符号整数*  
  
 *无符号整数*:: =*数字...*  
  
 *加号*:: = *+*  
  
 *负号*:: =-  
  
 *数字*:: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *段*:: =。
