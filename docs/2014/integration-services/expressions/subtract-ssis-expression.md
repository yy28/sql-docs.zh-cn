---
title: '- （减）（SSIS 表达式）| Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
ms.assetid: b48da086-37dd-460a-8a4b-912f52c9b158
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03ede2272de2c574909ed44bb0291b3c56911f0b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62768723"
---
# <a name="--subtract-ssis-expression"></a>-（减）（SSIS 表达式）
  从第一个数值表达式的值中减去第二个数值表达式的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
numeric_expression1 - numeric_expression2  
  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression1、numeric_expression2*  
 是数值数据类型的任意有效表达式。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 由两个参数的数据类型决定。 有关详细信息，请参阅 [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md)。  
  
## <a name="remarks"></a>备注  
 用括号将减法一元表达式括起来，以便确保按正确顺序对该表达式进行求值。  
  
## <a name="remarks"></a>备注  
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
  
 此示例从 **ListPrice** 列中减去计算后的值。 变量 **Discount%** 必须用括号括起来，因为该名称中包含字符 %。 有关详细信息，请参阅[标识符 (SSIS)](identifiers-ssis.md)。  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](operators-ssis-expression.md)  
  
  
