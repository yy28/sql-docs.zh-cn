---
title: ^（位异或）（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- bitwise exclusive OR (^)
ms.assetid: 6ac53cab-29c4-4835-9f87-371b058b2f38
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8aa8033e8af22fa518ce8b5e27dde817395f7eaf
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58271151"
---
# <a name="-bitwise-exclusive-or-ssis-expression"></a>^（位异或）（SSIS 表达式）
  对两个整数值执行“位异或”运算。 它会将第一个操作数的每一位与第二个操作数中对应的每一位进行比较。 如果一位是 0，另一对应位是 1，则相应结果位设置为 1。 如果两位都是 0 或两位都是 1，则相应结果位设置为 0。  
  
 两个条件必须都为有符号的整数数据类型，或都为无符号的整数数据类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
integer_expression1 ^ integer_expression2  
  
```  
  
## <a name="arguments"></a>参数  
 *integer_expression1、integer_expression2*  
 是有符号或无符号整数数据类型的任意有效表达式。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 由两个参数的数据类型确定。 有关详细信息，请参阅 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)。  
  
## <a name="remarks"></a>Remarks  
 如果任一条件为 Null，则表达式的结果为 Null。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例对变量 **NumberA** 和 **NumberB**执行“位异或”运算。 **NumberA** 包含 3 (00000011)， **NumberB** 包含 7 (00000111)。  
  
```  
@NumberA ^ @NumberB  
```  
  
 表达式计算结果为 4 (00000100)。  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000100  
  
 此示例对 **ReorderPoint** 和 **SafetyStockLevel** 列执行“位异或”运算。  
  
```  
ReorderPoint ^ SafetyStockLevel  
```  
  
 如果 **ReorderPoint** 为 10，而 **SafetyStockLevel** 为 8，则表达式计算结果为 2 (00000010)。  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00000010  
  
 此示例对两个整数执行“位异或”运算。  
  
```  
3 ^ 5   
```  
  
 表达式计算结果为 6 (00000110)。  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000110  
  
## <a name="see-also"></a>另请参阅  
 [||（逻辑或）（SSIS 表达式）](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [|（位异或）（SSIS 表达式）](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)   
 [运算符优先级和结合性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
