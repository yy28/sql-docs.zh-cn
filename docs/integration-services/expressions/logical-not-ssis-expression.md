---
title: "! （逻辑非）（SSIS 表达式） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logical Not (!)
- '! (logical Not)'
ms.assetid: d5c4d1e1-7be4-4d25-bcd9-5b6ddb53b3b3
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 003e0fcc98a267342aaf7c77bf344cdfdc71880b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="-logical-not-ssis-expression"></a>! （逻辑非）（SSIS 表达式）
  对布尔操作数求反。  
  
> [!NOTE]  
>  此 ! 运算符不能与其他运算符一起使用。 例如，不能将 ! 和 > 运算符组合为 !>. 运算符。  
  
## <a name="syntax"></a>语法  
  
```  
  
!boolean_expression  
  
```  
  
## <a name="arguments"></a>参数  
 *boolean_expression*  
 计算结果为布尔值的任何有效表达式。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 DT_BOOL  
  
## <a name="remarks"></a>注释  
 下表显示了 ! 操作。  
  
|原始布尔表达式|应用 ! 运算符后的表达式|  
|---------------------------------|------------------------------------|  
|TRUE|FALSE|  
|NULL|NULL|  
|FALSE|TRUE|  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例中，如果 **Color** 列的值为“red”，则计算结果为 FALSE。  
  
```  
!(Color == "red")  
```  
  
 在以下示例中，如果 **MonthNumber** 变量的值和代表当前月份的整数相同，则计算结果为 TRUE。 有关详细信息，请参阅 [MONTH（SSIS 表达式）](../../integration-services/expressions/month-ssis-expression.md)和 [GETDATE（SSIS 表达式）](../../integration-services/expressions/getdate-ssis-expression.md)。  
  
```  
!(@MonthNumber != MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符优先级和结合性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [运算符 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

