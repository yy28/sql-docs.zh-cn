---
title: EXP（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 00aea33b9ee240229cc399650f4c227e86f19507
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52752099"
---
# <a name="exp-ssis-expression"></a>EXP（SSIS 表达式）
  返回数值表达式以 e 为基的指数。 EXP 函数是对 LN 函数操作的补充，有时称为反对数。  
  
## <a name="syntax"></a>语法  
  
```  
  
EXP(numeric_expression)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 有效的数值表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_R8  
  
## <a name="remarks"></a>备注  
 计算指数前数值表达式被转换为 DT_R8 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
 返回结果始终为正数。  
  
## <a name="expression-examples"></a>表达式示例  
 这些示例对正值、负值和零应用 EXP 函数。  
  
```  
EXP(74)  
```  
  
 返回 1.373382979540176E+32。  
  
```  
EXP(-27)  
```  
  
 返回 1.879528816539083E-12。  
  
```  
EXP(0)  
```  
  
 返回 1。  
  
## <a name="see-also"></a>请参阅  
 [LOG（SSIS 表达式）](log-ssis-expression.md)   
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
