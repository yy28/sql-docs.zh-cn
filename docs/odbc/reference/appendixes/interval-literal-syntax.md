---
title: 间隔文本语法 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3387b07a8e769206a6a495addff4287000691fec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290567"
---
# <a name="interval-literal-syntax"></a>间隔文本语法
以下语法用于 ODBC 中的间隔文本。  
  
 *间隔文本 ：：* INTERVAL* =*&#124;*-]*间隔-字符串间隔限定符*  
  
 *间隔字符串*：：**报价*=*年月文本*&#124;*日时文本*=*报价*  
  
 *年月文本*：：**年值*&#124; =*年值*-=*月值*  
  
 *日间文字*：：：**日时间隔*&#124;*时间间隔*  
  
 *日时间隔*：：**天值*=*小时值*[：*分钟值*]：*秒值**  
  
 *时间间隔*：：**小时值*[：*分钟值*[：*秒值*]  
  
 &#124;*分钟值*[：*秒值*]  
  
 &#124;*秒值*  
  
 *年值*：：**日期时间值*  
  
 *月值*：：**日期时间值*  
  
 *天值*：：**日期时间值*  
  
 *小时值*：：**日期时间值*  
  
 *分钟值*：：**日期时间值*  
  
 *秒值*：：=*秒-整数值*[.]*秒数分数*|]  
  
 *秒-整数值*：：**无符号整数*  
  
 *秒数分数*：：**无符号整数*  
  
 *日期时间值*：：**无符号整数*  
  
 *间隔限定符*：：**起始字段*到*结束字段*&#124;*单日期时间字段*  
  
 *起始字段*：：**非秒日期时间字段*[（*间隔前导场精度*）]  
  
 *结束字段*：：**非秒日期时间字段*&#124;秒精度]（*间隔-分数-秒精度*）]  
  
 *单日期时间字段*：：**非秒日期时间场*[（*间隔前导场精度*）] &#124;*interval-leading-field-precision* *interval-fractional-seconds-precision*  
  
 *日期时间字段*：：**非秒日期时间字段*&#124;  
  
 *非秒日期时间字段*：：* &#124;月份 &#124; 天 &#124; HOUR &#124; 分钟  
  
 *间隔分数-秒-精度*：：**无符号整数*  
  
 *间隔领先的场精度*：：**无符号整数*  
  
 *报价*：：*  
  
 *无符号整数*：：**数字...*
