---
title: 除（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- / (divide)
- divide operator (/)
ms.assetid: 5bde9223-872d-443e-8a27-57735e1d8f3d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bf72606d04d02cda0ec656509f56fc636ee1f6e5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52810189"
---
# <a name="divide-ssis-expression"></a>除（SSIS 表达式）
  用第一个数值表达式除以第二个数值表达式。  
  
## <a name="syntax"></a>语法  
  
```  
  
dividend / divisor  
  
```  
  
## <a name="arguments"></a>参数  
 *被除数*  
 被除数的数值表达式。 *dividend* 可以是任意有效的数值表达式。 有关详细信息，请参阅 [Integration Services Data Types](../data-flow/integration-services-data-types.md)。  
  
 *除数*  
 除数的数值表达式。 *divisor* 可以是除 0 之外的任意有效的数值表达式。  
  
## <a name="result-types"></a>结果类型  
 由两个参数的数据类型确定。 有关详细信息，请参阅 [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md)。  
  
## <a name="remarks"></a>备注  
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
  
## <a name="see-also"></a>请参阅  
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](operators-ssis-expression.md)  
  
  
