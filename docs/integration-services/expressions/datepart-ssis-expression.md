---
title: DATEPART（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- dates [Integration Services], DATEPART
- DATEPART function
ms.assetid: 3e590094-fc49-4144-805f-fdc1bf2fe509
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bcd15decfe2c2d1981c403a8f00daadb2232a240
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="datepart-ssis-expression"></a>DATEPART（SSIS 表达式）
  返回一个表示日期的日期部分的整数。  
  
## <a name="syntax"></a>语法  
  
```  
  
DATEPART(datepart, date)  
```  
  
## <a name="arguments"></a>参数  
 *datepart*  
 此参数指定需要对日期中的哪一部分返回新值。  
  
 *date*  
 返回有效日期或日期格式的字符串的表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 如果此参数为空，则 DATEPART 返回的结果为空。  
  
 日期文字必须显式转换为日期数据类型之一。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 下表列出了表达式计算器可以识别的日期部分和缩写形式。 日期部分名称不区分大小写。  
  
|datepart|缩写形式|  
|--------------|-------------------|  
|Year|yy、yyyy|  
|季度|qq、q|  
|Month|mm、m|  
|Dayofyear|dy、y|  
|Day|dd、d|  
|Week|wk、ww|  
|Weekday|dw|  
|Hour|Hh|  
|Minute|mi、n|  
|第二个|ss、s|  
|Millisecond|Ms|  
  
## <a name="ssis-expression-examples"></a>SSIS 表达式示例  
 此示例返回表示日期文字中的月的整数。 如果日期是“mm/dd/yyyy”格式，则此示例返回 11。  
  
```  
DATEPART("month", (DT_DBTIMESTAMP)"11/04/2002")  
```  
  
 此示例返回 **ModifiedDate** 列中表示天的整数。  
  
```  
DATEPART("dd", ModifiedDate)  
```  
  
 此示例返回当前日期中表示年的整数。  
  
```  
DATEPART("yy",GETDATE())  
```  
  
## <a name="see-also"></a>另请参阅  
 [DATEADD（SSIS 表达式）](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF（SSIS 表达式）](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DAY（SSIS 表达式）](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH（SSIS 表达式）](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR（SSIS 表达式）](../../integration-services/expressions/year-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
