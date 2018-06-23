---
title: GETUTCDATE（SSIS 表达式）| Microsoft Docs
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
- dates [Integration Services], GETUTCDATE
- current date
- UTC time
- GETUTCDATE function
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 091063acbaea65d155e578ff6a4c21c95d941a39
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018897"
---
# <a name="getutcdate-ssis-expression"></a>GETUTCDATE（SSIS 表达式）
  使用 DT_DBTIMESTAMP 格式返回以 UTC 时间（协调世界时或格林尼治标准时间）表示的系统当前日期。 GETUTCDATE 函数不带参数。  
  
## <a name="syntax"></a>语法  
  
```  
  
GETUTCDATE()  
```  
  
## <a name="arguments"></a>参数  
 InclusionThresholdSetting  
  
## <a name="result-types"></a>结果类型  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>表达式示例  
 此示例返回以 UTC 时间表示的当前日期的年份。  
  
```  
DATEPART("year",GETUTCDATE())  
```  
  
 此示例返回 **ModifiedDate** 列中的日期和当前 UTC 日期之间的天数。  
  
```  
DATEDIFF("dd",ModifiedDate,GETUTCDATE())  
```  
  
 此示例将三个月加到当前 UTC 日期。  
  
```  
DATEADD("Month",3,GETUTCDATE())  
```  
  
## <a name="see-also"></a>请参阅  
 [GETDATE &#40;SSIS 表达式&#41;](getdate-ssis-expression.md)   
 [函数&#40;SSIS 表达式&#41;](functions-ssis-expression.md)  
  
  