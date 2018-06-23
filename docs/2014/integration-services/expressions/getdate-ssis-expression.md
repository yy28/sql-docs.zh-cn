---
title: GETDATE（SSIS 表达式）| Microsoft Docs
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
- current date
- GETDATE function
- dates [Integration Services], GETDATE
ms.assetid: 6d20ec93-3244-4d63-baf6-70eff7bd598c
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9161d114b9f103dc857c26a07b3c107d14a00b40
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128800"
---
# <a name="getdate-ssis-expression"></a>GETDATE（SSIS 表达式）
  以 DT_DBTIMESTAMP 格式返回系统的当前日期。 GETDATE 函数不使用参数。  
  
> [!NOTE]  
>  GETDATE 函数的返回结果的长度为 29 个字符。  
  
## <a name="syntax"></a>语法  
  
```  
  
GETDATE()  
```  
  
## <a name="arguments"></a>参数  
 InclusionThresholdSetting  
  
## <a name="result-types"></a>结果类型  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>表达式示例  
 此示例返回当前日期的年份。  
  
```  
DATEPART("year",GETDATE())  
```  
  
 此示例返回 **ModifiedDate** 列中的日期和当前日期之间的天数。  
  
```  
DATEDIFF("dd",ModifiedDate,GETDATE())  
```  
  
 此示例将三个月加到当前日期。  
  
```  
DATEADD("Month",3,GETDATE())  
```  
  
## <a name="see-also"></a>请参阅  
 [GETUTCDATE &#40;SSIS 表达式&#41;](getutcdate-ssis-expression.md)   
 [函数&#40;SSIS 表达式&#41;](functions-ssis-expression.md)  
  
  