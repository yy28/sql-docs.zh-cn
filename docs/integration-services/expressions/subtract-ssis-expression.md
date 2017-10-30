---
title: "- （减）（SSIS 表达式） |Microsoft 文档"
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
- '- (subtract)'
- subtract operator (-)
ms.assetid: b48da086-37dd-460a-8a4b-912f52c9b158
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d185d99f8ebd22d05446eadb556bd7ebcb95cb2f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="--subtract-ssis-expression"></a>-（减）（SSIS 表达式）
  从第一个数值表达式的值中减去第二个数值表达式的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
numeric_expression1 – numeric_expression2  
  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression1、numeric_expression2*  
 是数值数据类型的任意有效表达式。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 由两个参数的数据类型决定。 有关详细信息，请参阅 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)。  
  
## <a name="remarks"></a>注释  
 用括号将减法一元表达式括起来，以便确保按正确顺序对该表达式进行求值。  
  
## <a name="remarks"></a>注释  
 如果任意一个操作数为 Null，则结果为 Null。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例将数值相减。  
  
```  
5 - 6.09  
```  
  
 此示例从 **ListPrice** 列中的值中减去 **StandardCost** 列中的值。  
  
```  
ListPrice - StandardCost  
```  
  
 此示例从 **ListPrice** 列中减去计算后的值。 变量 **Discount%** 必须用括号括起来，因为该名称中包含字符 %。 有关详细信息，请参阅[标识符 (SSIS)](../../integration-services/expressions/identifiers-ssis.md)。  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符优先级和结合性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [运算符 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

