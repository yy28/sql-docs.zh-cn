---
title: 除（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- / (divide)
- divide operator (/)
ms.assetid: 5bde9223-872d-443e-8a27-57735e1d8f3d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 27a5fa59f2f7ba7b3ceac4eebb9547ebd8d32b6f
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58274772"
---
# <a name="divide-ssis-expression"></a>除（SSIS 表达式）
  用第一个数值表达式除以第二个数值表达式。  
  
## <a name="syntax"></a>语法  
  
```  
  
dividend / divisor  
  
```  
  
## <a name="arguments"></a>参数  
 *被除数*  
 被除数的数值表达式。 *dividend* 可以是任意有效的数值表达式。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 *除数*  
 除数的数值表达式。 *divisor* 可以是除 0 之外的任意有效的数值表达式。  
  
## <a name="result-types"></a>结果类型  
 由两个参数的数据类型确定。 有关详细信息，请参阅 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)。  
  
## <a name="remarks"></a>Remarks  
 如果任意一个操作数为 Null，则结果为 Null。  
  
 被零除是非法的。 根据 *divisor* 子表达式的计算方法，会出现下列错误之一：  
  
-   如果计算结果为零的 *divisor* 子表达式是常量，则错误将在设计时发生，导致表达式验证失败。  
  
-   如果计算结果为零的 *divisor* 子表达式包含变量（但不是输入列），则在包运行前此表达式所属组件的预执行验证将失败。  
  
-   如果计算结果为零的 *divisor* 子表达式包含输入列，则错误将在运行时发生，并根据数据流组件的错误流规则来处理错误。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例将两个数值相除。  
  
```  
25 / 5  
```  
  
 此示例用 **ListPrice** 列中的值除以 **StandardCost** 列中的值。  
  
```  
ListPrice / StandardCost  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符优先级和结合性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
