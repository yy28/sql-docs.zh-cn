---
title: "SIGN （SSIS 表达式） |Microsoft 文档"
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
- positive values [Integration Services]
- SIGN function
- negative values
ms.assetid: 1547db08-4329-4781-91c2-36898ed71b15
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3a926bddda6c86a7930a349915cc2a77602448b4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="sign-ssis-expression"></a>SIGN（SSIS 表达式）
  返回数值表达式的符号：正号 (+1)、负号 (-1) 或零 (0)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SIGN(numeric_expression)  
```  
  
## <a name="arguments"></a>参数  
 *numeric_expression*  
 是一个有效的有符号数值表达式。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 DT_I4  
  
## <a name="remarks"></a>注释  
 如果该参数为空，SIGN 返回的结果为空。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例返回数值的符号。 返回结果为 -1。  
  
```  
SIGN(-123.45)  
```  
  
 此示例返回从 **DealerPrice** 列减去 **StandardCost** 列的结果的符号。  
  
```  
SIGN(DealerPrice - StandardCost)  
```  
  
## <a name="see-also"></a>另请参阅  
 [函数 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

