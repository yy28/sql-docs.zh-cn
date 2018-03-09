---
title: "IIF (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IIF_TSQL
- IIF
dev_langs:
- TSQL
helpviewer_keywords:
- IIF function
ms.assetid: e3ccf8ed-1cec-43ac-90b7-d8597c24b050
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a7b58233c958d8ca9dc6b0fea9f9e69290d13679
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="logical-functions---iif-transact-sql"></a>逻辑函数-IIF (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，根据布尔表达式计算为 true 还是 false，返回其中一个值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
IIF ( boolean_expression, true_value, false_value )  
```  
  
## <a name="arguments"></a>参数  
 *boolean_expression*  
 一个有效的布尔表达式。  
  
 如果此参数不是布尔表达式，则引发一个语法错误。  
  
 *true_value*  
 要返回如果值*boolean_expression*计算结果为 true。  
  
 *false_value*  
 要返回如果值*boolean_expression*计算结果为 false。  
  
## <a name="return-types"></a>返回类型  
 返回的数据类型具有最高优先级中的类型从*true_value*和*false_value*。 有关详细信息，请参阅[数据类型优先级 (Transact-SQL)](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>注释  
 IIF 是一种用于编写 CASE 表达式的快速方法。 它将传递的布尔表达式计算为第一个参数，然后根据计算结果返回其他两个参数之一。 也就是说， *true_value*布尔表达式是否为 true，则返回与*false_value*返回布尔表达式如果为 false 或未知。 *true_value*和*false_value*可以是任何类型。 适用于布尔表达式、null 处理和返回类型的 CASE 表达式的相同规则也适用于 IIF。 有关详细信息，请参阅[用例 &#40;Transact SQL &#41;](../../t-sql/language-elements/case-transact-sql.md).  
  
 IIF 转换为 CASE 这一事实也影响此函数的行为的其他方面。 因为 CASE 表达式最多可嵌套 10 层，所以 IIF 语句最多也只能嵌套 10 层。 此外，IIF 将作为语义上等同的 CASE 表达式对其他服务器远程执行，且具备远程执行的 CASE 表达式的所有行为。  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-iif-example"></a>A. 简单 IIF 示例  
  
```  
DECLARE @a int = 45, @b int = 40;  
SELECT IIF ( @a > @b, 'TRUE', 'FALSE' ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------  
TRUE  
  
(1 row(s) affected)  
```  
  
### <a name="b-iif-with-null-constants"></a>B. 带有 NULL 常量的 IIF  
  
```  
SELECT IIF ( 45 > 30, NULL, NULL ) AS Result;  
```  
  
 此语句的结果是一个错误。  
  
### <a name="c-iif-with-null-parameters"></a>C. 具有 NULL 参数的 IIF  
  
```  
DECLARE @P INT = NULL, @S INT = NULL;  
SELECT IIF ( 45 > 30, @p, @s ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------  
NULL  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [用例 &#40;Transact SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [选择 &#40;Transact SQL &#41;](../../t-sql/functions/logical-functions-choose-transact-sql.md)  
  
  
