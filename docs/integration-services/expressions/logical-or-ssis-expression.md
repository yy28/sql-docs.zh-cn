---
description: '||（逻辑或）（SSIS 表达式）'
title: '||（逻辑或）（SSIS 表达式） | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- OR operator
- logical OR (||)
- '|| (logical OR)'
ms.assetid: a3c07c09-f121-4187-9617-b01adcf843c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b613adbf102e1103506e6d86efb3bf87d81d72eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88347543"
---
# <a name="-logical-or-ssis-expression"></a>||（逻辑或）（SSIS 表达式）

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  执行“逻辑或”运算。 如果条件之一或两个条件都为 TRUE，则表达式计算结果为 TRUE。  
  
## <a name="syntax"></a>语法  
  
```  
  
boolean_expression1 || boolean_expression2  
```  
  
## <a name="arguments"></a>参数  
 *boolean_expression1、boolean_expression2*  
 计算结果为 TRUE、FALSE 或 NULL 的任意有效表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_BOOL  
  
## <a name="remarks"></a>注解  
 下表显示了 || 运算符的结果。  
  
|结果|表达式|Expression|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|TRUE|true|FALSE|  
|FALSE|FALSE|FALSE|  
|Null|Null|Null|  
|TRUE|Null|TRUE|  
|Null|Null|false|  
  
## <a name="ssis-expression-examples"></a>SSIS 表达式示例  
 该示例使用 **StandardCost** 和 **ListPrice** 列。 如果 **StandardCost** 列的值小于 300 或者 **ListPrice** 列的值大于 500，则该示例计算结果为 TRUE。  
  
```  
StandardCost < 300 || ListPrice > 500  
```  
  
 该示例使用变量 **SPrice** 和 **LPrice** ，而不是数值。  
  
```  
StandardCost < @SPrice || ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>另请参阅  
 [|（位异或）（SSIS 表达式）](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)   
 [^（位异或）（SSIS 表达式）](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [运算符优先级和结合性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
