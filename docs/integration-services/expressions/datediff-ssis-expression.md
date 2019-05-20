---
title: DATEDIFF（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- DATEDIFF statement
- dates [Integration Services], DATEDIFF
ms.assetid: 449b327f-47c7-4709-8bc6-4ee9a35cc330
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 961feeb5714ae007d13517887b2fb6edb794b2be
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725514"
---
# <a name="datediff-ssis-expression"></a>DATEDIFF（SSIS 表达式）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  返回两个指定日期之间所跨的日期和时间边界的数目。 *datepart* 参数标识要比较的日期和时间边界。  
  
## <a name="syntax"></a>语法  
  
```  
  
DATEDIFF(datepart, startdate, endate)  
```  
  
## <a name="arguments"></a>参数  
 *datepart*  
 此参数指定对日期的哪一部分进行比较并为其返回值。  
  
 *startdate*  
 此参数表示间隔的开始日期。  
  
 *endate*  
 此参数表示间隔的结束日期。  
  
## <a name="result-types"></a>结果类型  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 下表列出了表达式计算器可以识别的日期部分和缩写形式。  
  
|datepart|缩写形式|  
|--------------|-------------------|  
|Year|yy、yyyy|  
|季度|qq、q|  
|Month|mm、m|  
|Dayofyear|dy、y|  
|Day|dd、d|  
|Week|wk、ww|  
|Weekday|dw、w|  
|Hour|Hh|  
|Minute|mi、n|  
|第二个|ss、s|  
|Millisecond|Ms|  
  
 如果任何参数为空，则 DATEDIFF 返回的结果为空。  
  
 日期文字必须显式转换为日期数据类型之一。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 如果日期无效、日期或时间单元不是字符串、开始日期不是日期或结束日期不是日期，都将发生错误。  
  
 如果结束日期早于开始日期，则此函数返回负数。 如果开始日期等于结束日期或两者在同一间隔内，则此函数返回零。  
  
## <a name="ssis-expression-examples"></a>SSIS 表达式示例  
 此示例计算两个日期文字之间的天数。 如果日期是“mm/dd/yyyy”格式，此函数返回 7。  
  
```  
DATEDIFF("dd", (DT_DBTIMESTAMP)"8/1/2003", (DT_DBTIMESTAMP)"8/8/2003")  
```  
  
 此示例返回一个日期文字与当前日期之间的月数。  
  
```  
DATEDIFF("mm", (DT_DBTIMESTAMP)"8/1/2003",GETDATE())  
```  
  
 此示例返回 **ModifiedDate** 列中的日期与 **YearEndDate** 变量之间的周数。 如果 **YearEndDate** 具有 **date** 数据类型，则不需要显式转换。  
  
```  
DATEDIFF("Week", ModifiedDate,@YearEndDate)  
```  
  
## <a name="see-also"></a>另请参阅  
 [DATEADD（SSIS 表达式）](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEPART（SSIS 表达式）](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY（SSIS 表达式）](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH（SSIS 表达式）](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR（SSIS 表达式）](../../integration-services/expressions/year-ssis-expression.md)   
 [函数（SSIS 表达式）](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
