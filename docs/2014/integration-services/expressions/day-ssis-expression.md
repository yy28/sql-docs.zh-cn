---
title: DAY（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- DAY function
- dates [Integration Services], DAY
ms.assetid: d8447187-49df-45b7-a98e-142ad44fd3e2
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b569d3114e89d623b896ed33a87aa95dc1cff32a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027937"
---
# <a name="day-ssis-expression"></a>DAY（SSIS 表达式）
  返回一个整数，表示日期的“日”日期部分。  
  
## <a name="syntax"></a>语法  
  
```  
  
DAY(date)  
```  
  
## <a name="arguments"></a>参数  
 *date*  
 返回有效日期或日期格式的字符串的表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 如果参数为空，则 DAY 将返回空结果。  
  
 日期文字必须显式转换为日期数据类型之一。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
> [!NOTE]  
>  在日期文本显式转换为以下日期数据类型之一时，表达式验证失败：DT_DBTIMESTAMPOFFSET 和 DT_DBTIMESTAMP2。  
  
 与 DATEPART("Day", date) 相比，DAY 函数效果相同，但更简洁。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例返回日期文字中的日期数字。 如果日期格式是“mm/dd/yyyy”格式，则此示例将返回 23。  
  
```  
DAY((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 此示例返回 **ModifiedDate** 列中表示天的整数。  
  
```  
DAY(ModifiedDate)  
```  
  
 以下示例返回表示当前日期的“日”部分的整数。  
  
```  
DAY(GETDATE())  
```  
  
## <a name="see-also"></a>请参阅  
 [DATEADD &#40;SSIS 表达式&#41;](dateadd-ssis-expression.md)   
 [DATEDIFF &#40;SSIS 表达式&#41;](datediff-ssis-expression.md)   
 [DATEPART（SSIS 表达式）](datepart-ssis-expression.md)   
 [MONTH（SSIS 表达式）](month-ssis-expression.md)   
 [YEAR（SSIS 表达式）](year-ssis-expression.md)   
 [函数&#40;SSIS 表达式&#41;](functions-ssis-expression.md)  
  
  