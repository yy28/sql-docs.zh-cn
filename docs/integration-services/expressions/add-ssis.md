---
title: + +（加）(SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- + (add)
- add operator (+)
- adding expressions
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e7f51d8027bcb65b1f9e3596748778baed36759e
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270946"
---
# <a name="-add-ssis"></a>+（加）(SSIS)
  将两个数值表达式相加。  
  
## <a name="syntax"></a>语法  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression1、numeric_expression2*  
 是数值数据类型的任意有效表达式。  
  
## <a name="result-types"></a>结果类型  
 由两个参数的数据类型确定。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="remarks"></a>Remarks  
 如果任意一个操作数为 Null，则结果为 Null。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例将数值相加。  
  
```  
5 + 6.09 + 7.0  
```  
  
 此示例将 **VacationHours** 和 **SickLeaveHours** 列中的值相加。  
  
```  
VacationHours + SickLeaveHours  
```  
  
 此示例将计算后的值添加到 **StandardCost** 列。 变量 **Profit%** 必须用方括号括起来，因为该名称包含 % 字符。 有关详细信息，请参阅[标识符 (SSIS)](../../integration-services/expressions/identifiers-ssis.md)。  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符优先级和结合性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
