---
title: （取模）（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '% (modulo operator)'
- remainder of division operation
- modulo operator (%)
ms.assetid: e2920821-2f5b-4c76-8db8-8b9eddf4606f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 163dbfecd4605c6c9624d94c047b1c7e893d8fcd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62768873"
---
# <a name="modulo-ssis-expression"></a>（取模）（SSIS 表达式）
  将第一个数据表达式的值除以第二个数据表达式的值后，提供整数余数。  
  
## <a name="syntax"></a>语法  
  
```  
  
dividend % divisor  
  
```  
  
## <a name="arguments"></a>参数  
 *被除数*  
 被除数的数值表达式。 *dividend* 可以是任意有效的数值表达式。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
 *除数*  
 除数的数值表达式。 *divisor* 可以是除 0 之外的任意有效的数值表达式。  
  
## <a name="result-types"></a>结果类型  
 由两个参数的数据类型确定。 有关详细信息，请参阅 [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md)。  
  
## <a name="remarks"></a>备注  
 两个表达式的计算结果必须为有符号或无符号整数数据类型。  
  
 如果任意一个操作数为 Null，则结果为 Null。  
  
 不可对零取模。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例对两个数值取模。 结果为 3。  
  
```  
42 % 13  
```  
  
 以下示例对 **SalesQuota** 列和一个数值文字取模。  
  
```  
SalesQuota % 12  
```  
  
 以下示例对两个数值变量 **Sales$** 和 **Month**取模。 变量 **Sales$** 的名称包含 $ 字符，所以必须括在括号内。 有关详细信息，请参阅[标识符 (SSIS)](identifiers-ssis.md)。  
  
```  
@[Sales$] % @Month  
```  
  
 以下示例使用取模运算符确定 **Value** 变量的值为偶数还是奇数，并使用条件运算符返回对结果进行说明的字符串。 有关详细信息，请参阅 [?：（条件）（SSIS 表达式）](conditional-ssis-expression.md)。  
  
```  
@Value % 2 == 0? "even":"odd"  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](operators-ssis-expression.md)  
  
  
