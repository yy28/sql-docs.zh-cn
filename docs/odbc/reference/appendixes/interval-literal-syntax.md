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
ms.openlocfilehash: 6352a5ae894adb09f714a78386bfecfa3ce1df77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041620"
---
# <a name="interval-literal-syntax"></a>间隔文本语法
下面的语法用于 ODBC 中的间隔文本。  
  
 *间隔文本：： = interval* [+*&#124;*]*间隔-字符串间隔-限定符*  
  
 *间隔-string* ：： =*引号*{*年月*&#124;*日期-文本*}*引号*  
  
 *年-文本*：： =*年-值*&#124; [*年-值*]*月-值*  
  
 *日期-文本*：： =*日期时间间隔*&#124;*时间间隔*  
  
 *日期-时间间隔*：： =*天-值*[*小时-值*[：*分钟-值*[：*秒-值*]]]  
  
 *时间间隔*：： =*小时-值*[：*分钟-值*[：*秒-值*]]  
  
 &#124;*分钟-值*[：*秒-值*]  
  
 &#124;*秒-值*  
  
 *年-值*：： = *datetime-值*  
  
 *月份-值*：： = *datetime-值*  
  
 *days-值*：： = *datetime-值*  
  
 *小时-值*：： = *datetime-值*  
  
 *分钟-值*：： = *datetime-值*  
  
 *秒-值*：： =*秒-整数值*[. [*秒-分式*]]  
  
 *秒钟-值*：： =*无符号整数*  
  
 *seconds-分式*：： =*无符号整数*  
  
 *datetime-value* ：： =*无符号整数*  
  
 *间隔-限定符*：： =*起始字段*到*结束字段*&#124;*单日期时间字段*  
  
 *起始-字段*：： =*非第二个日期/时间字段*[（*间隔-前导字段精度*）]  
  
 *结束字段*：： =*非第二个日期/时间字段*&#124; 第二个 [（*间隔-秒-精度*）]  
  
 *单时间-字段*：： =*非第二个日期/时间字段*[（*时间间隔-前导字段精度*）] &#124; 第二个 [（时间间隔-*字段*精度 [，（*间隔-秒-精度-精度*）]  
  
 *datetime-field* ：： =*非 second-datetime-field* &#124; second  
  
 *非第一个日期时间字段*：： = 年 &#124; 月 &#124; 天 &#124; 小时 &#124; 分钟  
  
 *间隔-秒-精度*：： =*无符号整数*  
  
 *间隔-行距*：： =*无符号整数*  
  
 *quote* ：： = '  
  
 *无符号整数*：： =*数字 ...*
