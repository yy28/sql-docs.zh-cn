---
title: '|（位或）（SSIS 表达式）| Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '| (bitwise inclusive OR)'
- bitwise inclusive OR (|)
ms.assetid: 4dce9eb2-3680-4adc-81a3-816ea52cef49
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a7424c52583ebe5f2a886eba19c33c0749cf9f88
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967487"
---
# <a name="-bitwise-inclusive-or-ssis-expression"></a>|（位或）（SSIS 表达式）
  对两个整数值执行“位或”运算。 它会将第一个操作数的每一位与第二个操作数中对应的每一位进行比较。 如果任一位为 1，则对应结果位设置为 1。 否则，相应的结果位设置为零 (0)。  
  
 两个条件必须都为有符号的整数数据类型，或都为无符号的整数数据类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
integer_expression1 | integer_expression2  
  
```  
  
## <a name="arguments"></a>参数  
 *integer_expression1、integer_expression2*  
 是有符号或无符号整数数据类型的任意有效表达式。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 由两个参数的数据类型确定。 有关详细信息，请参阅 [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md)。  
  
## <a name="remarks"></a>备注  
 如果任一条件为 Null，则表达式的结果为 Null。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例对变量 **NumberA** 和 **NumberB**执行“位或”运算。 **NumberA** 包含 3 (00000011)， **NumberB** 包含 9 (00001001)。  
  
```  
@NumberA | @NumberB  
```  
  
 表达式的计算结果为 11 (00001011)。  
  
 00000011  
  
 00001001  
  
 ----------\-  
  
 00001011  
  
 此示例对 **ReorderPoint** 和 **SafetyStockLevel** 列执行“位或”运算。  
  
```  
ReorderPoint | SafetyStockLevel  
```  
  
 如果 **ReorderPoint** 为 10，而 **SafetyStockLevel** 为 8，则表达式计算结果为 10 (00001010)。  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001010  
  
 此示例对两个整数执行“位或”运算。  
  
```  
3 | 5   
```  
  
 表达式的计算结果为 7 (00000111)。  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000111  
  
## <a name="see-also"></a>另请参阅  
 [||（逻辑或）（SSIS 表达式）](logical-or-ssis-expression.md)   
 [^（位异或）（SSIS 表达式）](bitwise-exclusive-or-ssis-expression.md)   
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](operators-ssis-expression.md)  
  
  
