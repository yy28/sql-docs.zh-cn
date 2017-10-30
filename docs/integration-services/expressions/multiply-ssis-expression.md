---
title: "* （乘）（SSIS 表达式） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- '* (multiply operator)'
- multiply operator (*)
ms.assetid: d457f052-ffbb-4485-833f-f4bed4349b69
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bb439e9221a1bcb169776eec1f6251b49ed4b861
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="-multiply-ssis-expression"></a>*（乘）（SSIS 表达式）
  将两个数值表达式相乘。  
  
## <a name="syntax"></a>语法  
  
```  
  
numeric_expression1 * numeric_expression2  
  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression1、numeric_expression2*  
 是数值数据类型的任意有效表达式。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 由两个参数的数据类型确定。 有关详细信息，请参阅 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)。  
  
## <a name="remarks"></a>注释  
 如果任意一个操作数为 Null，则结果为 Null。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例将数值相乘。  
  
```  
5 * 6.09  
```  
  
 以下示例将 **ListPrice** 列中的值乘以 10%。  
  
```  
ListPrice * .10  
```  
  
 以下示例从 **ListPrice** 列减去表达式的结果。 变量 **Discount%** 必须用括号括起来，因为该名称中包含字符 %。 有关详细信息，请参阅[标识符 (SSIS)](../../integration-services/expressions/identifiers-ssis.md)。  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符优先级和结合性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [运算符 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

