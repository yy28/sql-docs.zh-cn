---
title: 间隔文本语法 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], interval
- interval literals [ODBC]
- ODBC literals [ODBC], interval
ms.assetid: 2f2d22c1-51d6-4055-9f5a-53bc31e9fea0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d477dbc6b54d7ebd82b7e2ef8611f5f6dd807e83
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694042"
---
# <a name="interval-literal-syntax"></a>间隔文本语法
以下语法用于间隔 ODBC 中的文本。  
  
 *间隔文本:: = 间隔*[+*&#124;*-]*时间间隔字符串间隔限定符*  
  
 *时间间隔字符串*:: =*报价*{*年-月-文本* &#124; *天时间文字*}*引号*  
  
 *年-月-文字*:: =*年份值* &#124; [*年份值*-]*月数值*  
  
 *日期时间文字*:: =*天时间间隔* &#124; *时间间隔*  
  
 *一天时间间隔*:: =*天数值*[*小时值*[:*分钟值*[:*秒值*]]]  
  
 *时间间隔*:: =*小时值*[:*分钟值*[:*秒值*]]  
  
 &#124;*分钟值*[:*秒值*]  
  
 &#124;*秒值*  
  
 *年份值*:: =*日期时间值*  
  
 *月数值*:: =*日期时间值*  
  
 *天数值*:: =*日期时间值*  
  
 *小时值*:: =*日期时间值*  
  
 *分钟值*:: =*日期时间值*  
  
 *秒值*:: =*秒的整数值*[。 [*秒部分*]]  
  
 *秒的整数值*:: =*无符号整数*  
  
 *秒部分的前*:: =*无符号整数*  
  
 *日期时间值*:: =*无符号整数*  
  
 *间隔限定符*:: =*开始字段*TO*结束字段* &#124; *单日期时间字段*  
  
 *开始字段*:: =*非-秒的日期时间的字段*[(*间隔前导字段精度*)]  
  
 *结束字段*:: =*非-秒的日期时间的字段*&#124;第二个 [(*间隔的小数部分的秒的精度*)]  
  
 *单个日期时间字段*:: =*非-秒的日期时间的字段*[(*间隔前导字段精度*)]&#124;第二个 [(*间隔前导字段精度* [，(*时间间隔的小数部分的秒的精度*)]  
  
 *日期时间字段*:: =*非-秒的日期时间的字段*&#124;第二个  
  
 *非-秒的日期时间的字段*:: = 年&#124;月&#124;天&#124;小时&#124;分钟  
  
 *时间间隔的小数部分的秒的精度*:: =*无符号整数*  
  
 *间隔前导字段精度*:: =*无符号整数*  
  
 *引号*:: =  
  
 *无符号整数*:: =*数字...*
