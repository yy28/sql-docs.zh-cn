---
title: POWER（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- POWER function
ms.assetid: db48ae65-bfa6-4db1-8d3c-d0d4f8a399bc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5c89408e2d1bd840bc2dac5d7cf27486569f40de
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428294"
---
# <a name="power-ssis-expression"></a>POWER（SSIS 表达式）
  返回对数值表达式进行幂运算的结果。 Power 参数的计算结果必须为整数。  
  
## <a name="syntax"></a>语法  
  
```  
  
POWER(numeric_expression,power)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 有效的数值表达式。  
  
 *power*  
 有效的数值表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_R8  
  
## <a name="remarks"></a>备注  
 执行幂运算前， *numeric_expression* 和 *power* 参数会转换为 DT_R8 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
 如果 *numeric_expression* 的计算结果为零，并且 *power* 为负，则表达式计算器将返回错误，并将返回结果设置为 Null。  
  
 如果 *numeric_expression* 或 *power* 的计算结果不确定，则返回结果为 Null。  
  
 *power* 参数可以是小数。 例如，可以使用 0.5 作为幂值。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例使用了一个数值。 该函数计算 4 的 3 次幂，返回 64。  
  
```  
POWER(4,3)  
```  
  
 以下示例使用了 **Length** 列和 **DimensionCount** 变量。 如果 **Length** 为 8， **DimensionCount** 为 2，则返回结果为 64。  
  
```  
POWER(Length, @DimensionCount)   
```  
  
## <a name="see-also"></a>另请参阅  
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
