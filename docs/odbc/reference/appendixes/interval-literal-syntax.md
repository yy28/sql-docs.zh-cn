---
title: 间隔文本语法 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], interval
- interval literals [ODBC]
- ODBC literals [ODBC], interval
ms.assetid: 2f2d22c1-51d6-4055-9f5a-53bc31e9fea0
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4f0d7155a5ba476906bc1d8453b7732d8d5b45c1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="interval-literal-syntax"></a>间隔文本语法
以下语法用于 ODBC 中的间隔文本。  
  
 *间隔文本:: = 间隔*[+*&#124;*-]*间隔字符串间隔限定符*  
  
 *间隔字符串*:: =*引号*{*年-月-文本* &#124; *天时间文字*}*引号*  
  
 *年-月-文本*:: =*年份值* &#124; [*年份值*-]*月数值*  
  
 *一天时间文字*:: =*天时间间隔* &#124; *时间间隔*  
  
 *一天时间间隔*:: =*天数值*[*小时值*[:*分钟值*[:*秒值*]]]  
  
 *时间间隔*:: =*小时值*[:*分钟值*[:*秒值*]]  
  
 &#124;*分钟值*[:*秒值*]  
  
 &#124;*秒值*  
  
 *年份值*:: =*日期时间值*  
  
 *月数值*:: =*日期时间值*  
  
 *天数值*:: =*日期时间值*  
  
 *小时值*:: =*日期时间值*  
  
 *分钟值*:: =*日期时间值*  
  
 *秒值*:: =*秒整数值*[。 [*秒部分*]]  
  
 *秒整数值*:: =*无符号整数*  
  
 *秒部分*:: =*无符号整数*  
  
 *日期时间值*:: =*无符号整数*  
  
 *间隔限定符*:: =*开始字段*收件人*结束字段* &#124; *单日期时间字段*  
  
 *开始字段*:: =*非-秒-datetime-字段*[(*间隔前导字段精度*)]  
  
 *结束字段*:: =*非-秒-datetime-字段*&#124;第二个 [(*间隔小数部分组成的秒的精度*)]  
  
 *单 datetime 字段*:: =*非-秒-datetime-字段*[(*间隔前导字段精度*)]&#124;第二个 [(*间隔前导字段精度* [，(*间隔小数部分组成的秒的精度*)]  
  
 *datetime 字段*:: =*非-秒-datetime-字段*&#124;第二个  
  
 *非-秒-datetime-字段*:: = 年&#124;月&#124;天&#124;小时&#124;分钟  
  
 *时间间隔的小数部分组成的秒的精度*:: =*无符号整数*  
  
 *间隔前导字段精度*:: =*无符号整数*  
  
 *引号*:: =  
  
 *无符号整数*:: =*数字...*
