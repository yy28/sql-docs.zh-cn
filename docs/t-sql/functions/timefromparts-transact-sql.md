---
title: "TIMEFROMPARTS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TIMEFROMPARTS_TSQL
- TIMEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- TIMEFROMPARTS function
ms.assetid: 786c65a1-2b3f-4e4b-82b6-4940d62f3801
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: e7cb7497251a0a61cff9f71c07d3c5d9e9028d5d
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="timefromparts-transact-sql"></a>TIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  返回**时间**值指定的时间并使用指定的精度。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
TIMEFROMPARTS ( hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>参数  
 *小时*  
 用于指定小时的整数表达式。  
  
 *分钟*  
 用于指定分钟的整数表达式。  
  
 *seconds*  
 用于指定秒的整数表达式。  
  
 *分数 （竖式)*  
 用于指定小数部分的整数表达式。  
  
 *精度*  
 指定的精度的整数文本**时间**要返回值。  
  
## <a name="return-types"></a>返回类型  
 **时间 (** *精度* **)**  
  
## <a name="remarks"></a>注释  
 TIMEROMPARTS 返回完全初始化的时间值。 如果参数无效，则引发错误。 如果任何参数都为 null，则返回 null。 但是，如果*精度*自变量为 null，则引发错误。  
  
 *分数 （竖式)*取决于自变量*精度*自变量。 例如，如果*精度*为 7，则每个部分表示 100 纳秒; 如果*精度*为 3，则每个部分表示以毫秒为单位。 如果值*精度*为零，则值*分数 （竖式)*还必须为零; 否则，将引发错误。  
  
 此函数可以在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更高版本的服务器上远程执行。 它不能是远程访问服务器具有的版本低于[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. 不包含秒的小数部分的简单示例  
  
```  
SELECT TIMEFROMPARTS ( 23, 59, 59, 0, 0 ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------------------  
23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. 包含秒的小数部分的示例  
 下面的示例演示了利用*分数 （竖式)*和*精度*参数：  
  
1.  当*分数 （竖式)*的值为 5 和*精度*具有值为 1，然后将值*分数 （竖式)*表示 5/10 的第二个。  
  
2.  当*分数 （竖式)*的值为 50 和*精度*具有值为 2，然后将值*分数 （竖式)*表示的第二个 50/100。  
  
3.  当*分数 （竖式)*的值为 500 和*精度*具有值 3，然后将值*分数 （竖式)*表示 500/1000 的第二个。  
  
```tsql  
SELECT TIMEFROMPARTS ( 14, 23, 44, 5, 1 );  
SELECT TIMEFROMPARTS ( 14, 23, 44, 50, 2 );  
SELECT TIMEFROMPARTS ( 14, 23, 44, 500, 3 );  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------  
14:23:44.5  
  
(1 row(s) affected)  
  
----------------  
14:23:44.50  
  
(1 row(s) affected)  
  
----------------  
14:23:44.500  
  
(1 row(s) affected)  
```  
  


