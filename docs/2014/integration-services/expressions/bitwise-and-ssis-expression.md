---
title: '&amp;（位算符 AND）（SSIS 表达式）| Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 06d2958e-66a5-44d8-8bc4-56209ebe1ff2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f4785967ceafd105e8d7b56e24223edd40d08850
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374874"
---
# <a name="amp-bitwise-and-ssis-expression"></a>&amp;（位算符 AND）（SSIS 表达式）
  对两个整数值执行“位与”运算。 它会将第一个操作数的每一位与第二个操作数中对应的每一位进行比较。 如果两位都是 1，则相应的结果位设置为 1。 否则，相应的结果位设置为 0。  
  
 两个条件都必须是有符号整数类型，或者都必须是无符号整数类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
integer_expression1 & integer_expression2  
  
```  
  
## <a name="arguments"></a>参数  
 *integer_expression1、integer_expression2*  
 是有符号或无符号整数数据类型的任意有效表达式。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 由两个参数的数据类型确定。 有关详细信息，请参阅 [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md)。  
  
## <a name="remarks"></a>备注  
 如果任一条件为 Null，则表达式的结果为 Null。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例对 **NumberA** 和 **NumberB**列执行“位与”运算。 **NumberA** 列包含 3 (0000011)， **NumberB** 列包含 7 (00000111)。  
  
```  
NumberA & NumberB  
```  
  
 表达式计算结果为 3 (00000011)。  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000011  
  
 此示例对 **ReorderPoint** 和 **SafetyStockLevel** 列执行“位与”运算。  
  
```  
ReorderPoint & SafetyStockLevel  
```  
  
 如果 **ReorderPoint** 为 10，而 **SafetyStockLevel** 为 8，则表达式计算结果为 8 (00001000)。  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001000  
  
 此示例对两个整数执行“位与”运算。  
  
```  
3 & 5   
```  
  
 表达式计算结果为 1 (00000001)。  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000001  
  
## <a name="see-also"></a>请参阅  
 [&&（逻辑 AND）（SSIS 表达式）](logical-and-ssis-expression.md)   
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](operators-ssis-expression.md)  
  
  
