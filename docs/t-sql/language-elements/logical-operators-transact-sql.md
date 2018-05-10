---
title: 逻辑运算符 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], logical
- testing truth
- truth testing
- "TRUE"
- "FALSE"
- logical operators [SQL Server], Transact-SQL
ms.assetid: edd92f08-76fb-4fd7-a4b6-8520d6a81df1
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4f3a1f0170807ca0560c2253ecd578a848388c85
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="logical-operators-transact-sql"></a>逻辑运算符 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  逻辑运算符对某些条件进行测试，以获得其真实情况。 逻辑运算符和比较运算符一样，返回带有 TRUE、FALSE 或 UNKNOWN 值的布尔数据类型。  
  
|运算符|含义|  
|--------------|-------------|  
|[ALL](../../t-sql/language-elements/all-transact-sql.md)|如果一组的比较都为 TRUE，那么就为 TRUE。|  
|[AND](../../t-sql/language-elements/and-transact-sql.md)|如果两个布尔表达式都为 TRUE，那么就为 TRUE。|  
|[ANY](../../t-sql/language-elements/any-transact-sql.md)|如果一组的比较中任何一个为 TRUE，那么就为 TRUE。|  
|[BETWEEN](../../t-sql/language-elements/between-transact-sql.md)|如果操作数在某个范围之内，那么就为 TRUE。|  
|[EXISTS](../../t-sql/language-elements/exists-transact-sql.md)|如果子查询包含一些行，那么就为 TRUE。|  
|[IN](../../t-sql/language-elements/in-transact-sql.md)|如果操作数等于表达式列表中的一个，那么就为 TRUE。|  
|[LIKE](../../t-sql/language-elements/like-transact-sql.md)|如果操作数与一种模式相匹配，那么就为 TRUE。|  
|[NOT](../../t-sql/language-elements/not-transact-sql.md)|对任何其他布尔运算符的值取反。|  
|[或](../../t-sql/language-elements/or-transact-sql.md)|如果两个布尔表达式中的一个为 TRUE，那么就为 TRUE。|  
|[SOME](../../t-sql/language-elements/some-any-transact-sql.md)|如果在一组比较中，有些为 TRUE，那么就为 TRUE。|  
  
## <a name="see-also"></a>另请参阅  
 [运算符优先级 (Transact-SQL)](../../t-sql/language-elements/operator-precedence-transact-sql.md)  
  
  
