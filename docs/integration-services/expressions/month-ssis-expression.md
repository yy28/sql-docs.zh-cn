---
title: "MONTH （SSIS 表达式） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dates [Integration Services], MONTH
- MONTH function
ms.assetid: b5a47a11-c2ef-49bd-bd70-235632ff7bf6
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e2e480bc53181fdf01a64716e1fdb94fe4116716
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="month-ssis-expression"></a>MONTH（SSIS 表达式）
  返回一个表示日期中的“月份”日期部分的整数。  
  
## <a name="syntax"></a>语法  
  
```  
  
MONTH(date)  
```  
  
## <a name="arguments"></a>参数  
 *date*  
 是任意日期格式的日期。  
  
## <a name="result-types"></a>结果类型  
 DT_I4  
  
## <a name="remarks"></a>注释  
 如果参数为空，则 MONTH 返回的结果为空。  
  
 日期文字必须显式转换为日期数据类型之一。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
> [!NOTE]  
>  在日期文本显式转换为以下日期数据类型之一时，表达式验证失败：DT_DBTIMESTAMPOFFSET 和 DT_DBTIMESTAMP2。  
  
 使用 MONTH 函数更为简要，但等价于使用 DATEPART("Month", date)。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例返回日期文字中表示月份的数字。 如果日期是“mm/dd/yyyy”格式，则此示例返回 11。  
  
```  
MONTH((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 此示例返回 **ModifiedDate** 列中表示月份的整数。  
  
```  
MONTH(ModifiedDate)  
```  
  
 此示例返回表示当前日期中的月份的整数。  
  
```  
MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>另请参阅  
 [DATEADD &#40;SSIS 表达式 &#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;SSIS 表达式 &#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [日期部分 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [天 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [年 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [函数 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
