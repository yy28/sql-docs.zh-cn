---
title: LTRIM（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- leading blanks
- LTRIM function
ms.assetid: d082f42a-d7e7-49f5-a503-ac44ba630832
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 541531de470991c84d04a60d6829e3333c78ae3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62897494"
---
# <a name="ltrim-ssis-expression"></a>LTRIM（SSIS 表达式）
  返回删除了前导空格的字符表达式。  
  
> [!NOTE]  
>  LTRIM 不删除空格字符，如制表符或换行符。 Unicode 针对许多不同类型的空格提供了码位，但是该函数仅识别 Unicode 码位 0x0020。 双字节字符集 (DBCS) 字符串转换为 Unicode 时，它们可能包含 0x0020 之外的空格字符，而该函数无法删除此类空格。 若要删除所有类型的空格，可以在从脚本组件运行的脚本中使用 Microsoft Visual Basic .NET LTrim 方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
LTRIM(character expression)  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 要从中删除空格的字符表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_WSTR  
  
## <a name="remarks"></a>备注  
 LTRIM 只可用于 DT_WSTR 数据类型。 如果 *character_expression* 参数是字符串文字或数据类型为 DT_STR 的数据列，则它在 LTRIM 执行操作前隐式转换为 DT_WSTR 数据类型。 其他数据类型必须显式转换为 DT_WSTR 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)和[转换（SSIS 表达式）](cast-ssis-expression.md)。  
  
 如果参数为空，LTRIM 将返回空结果。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例将删除字符串文字中的前导空格。 返回结果为“Hello”。  
  
```  
LTRIM("    Hello")  
```  
  
 以下示例将删除 **FirstName** 列中的前导空格。  
  
```  
LTRIM(FirstName)  
```  
  
 以下示例将删除 **FirstName** 变量中的前导空格。  
  
```  
LTRIM(@FirstName)  
```  
  
## <a name="see-also"></a>请参阅  
 [RTRIM（SSIS 表达式）](trim-ssis-expression.md)   
 [TRIM（SSIS 表达式）](trim-ssis-expression.md)   
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
