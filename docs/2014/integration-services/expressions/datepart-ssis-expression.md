---
title: DATEPART（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], DATEPART
- DATEPART function
ms.assetid: 3e590094-fc49-4144-805f-fdc1bf2fe509
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 22225f9a1791185ed78dfc75d92c3dbced7be3ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62769334"
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
  
## <a name="remarks"></a>备注  
 如果此参数为空，则 DATEPART 返回的结果为空。  
  
 日期文字必须显式转换为日期数据类型之一。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
 下表列出了表达式计算器可以识别的日期部分和缩写形式。 日期部分名称不区分大小写。  
  
|datepart|缩写形式|  
|--------------|-------------------|  
|年龄|yy、yyyy|  
|季度|qq、q|  
|月份|mm、m|  
|Dayofyear|dy、y|  
|日期|dd、d|  
|Week|wk、ww|  
|星期|dw|  
|Hour|Hh|  
|Minute|mi、n|  
|秒|ss、s|  
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
 [DATEADD（SSIS 表达式）](dateadd-ssis-expression.md)   
 [DATEDIFF（SSIS 表达式）](datediff-ssis-expression.md)   
 [DAY（SSIS 表达式）](day-ssis-expression.md)   
 [MONTH（SSIS 表达式）](month-ssis-expression.md)   
 [YEAR（SSIS 表达式）](year-ssis-expression.md)   
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
