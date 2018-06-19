---
title: REPLACENULL（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 70db7832-b5a0-4db5-a8ad-42ad8630d8e8
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 27891900bfde62e758b265ef868cb77e0f56dbb1
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35332821"
---
# <a name="replacenull-ssis-expression"></a>REPLACENULL（SSIS 表达式）
  如果第一个表达式参数的值为 NULL，则返回第二个表达式参数的值；否则，返回第一个表达式的值。  
  
## <a name="syntax"></a>语法  
  
```vb  
REPLACENULL(expression 1,expression 2)  
```  
  
## <a name="arguments"></a>参数  
 *表达式 1*  
 检查此表达式的结果是否为 NULL。  
  
 *表达式 2*  
 如果第一个表达式的计算结果为 NULL，则返回此表达式的结果。  
  
## <a name="result-types"></a>结果类型  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
  
-   *expression 2* 的长度可以为零。  
  
-   如果任何参数为 Null，则 REPLACENULL 的返回结果为 Null。  
  
-   任一参数都不支持 BLOB 列（DT_TEXT、DT_NTEXT、DT_IMAGE）。  
  
-   两个表达式的返回类型应相同。 如果不相同，则函数尝试将第二个表达式的返回类型转换为第一个表达式的返回类型，如果数据类型不兼容，这可能会导致出现错误。  
  
## <a name="expression-examples"></a>表达式示例  
 下面的示例将数据库列中的任何 NULL 值替换为字符串 (1900-01-01)。 此函数专用在常见的“派生列”模式中，在该模式中，您可以将 NULL 值替换为其他值。  
  
```  
REPLACENULL(MyColumn, "1900-01-01")  
```  
  
> [!NOTE]  
>  下面的示例演示此函数在 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]/[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]中的实现方式。  
  
```  
(DT_DBTIMESTAMP) (ISNULL(MyColumn) ? “1900-01-01” : MyColumn)   
```  
  
  
