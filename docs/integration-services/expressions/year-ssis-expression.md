---
title: "YEAR （SSIS 表达式） |Microsoft 文档"
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
- dates [Integration Services], YEAR
- YEAR function
ms.assetid: 9d88dead-ace8-44b9-b8e2-916c1842e155
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a72a54b02f136f2d9acc130051e79852d72a2f1f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="year-ssis-expression"></a>YEAR（SSIS 表达式）
  返回一个表示日期中的“年份”日期部分的整数。  
  
## <a name="syntax"></a>语法  
  
```  
  
YEAR(date)  
```  
  
## <a name="arguments"></a>参数  
 *date*  
 是任意日期格式的日期。  
  
## <a name="result-types"></a>结果类型  
 DT_I4  
  
## <a name="remarks"></a>注释  
 如果参数为空，则 YEAR 返回的结果为空。  
  
 日期文字必须显式转换为日期数据类型之一。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
> [!NOTE]  
>  在日期文本显式转换为以下日期数据类型之一时，表达式验证失败：DT_DBTIMESTAMPOFFSET 和 DT_DBTIMESTAMP2。  
  
 使用 YEAR 函数更为简要，但其等价于使用 DATEPART("Year", date) 函数。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例返回日期文字中表示年份的数字。 如果日期格式为 mm/dd/yyyy，则此示例返回“2002”。  
  
```  
YEAR((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 此示例返回 **ModifiedDate** 列中表示年份的整数。  
  
```  
YEAR(ModifiedDate)  
```  
  
 此示例返回当前日期中表示年的整数。  
  
```  
YEAR(GETDATE())  
```  
  
## <a name="see-also"></a>另请参阅  
 [DATEADD &#40;SSIS 表达式 &#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;SSIS 表达式 &#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [日期部分 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [天 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [月 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [函数 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

