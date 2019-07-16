---
title: 错误 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 91d07c6bbb4eb4731c9a802e47cd8f4c71aa5aeb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031235"
---
# <a name="error-mdx"></a>Error (MDX)


  引发错误，根据需要可以选择提供指定的错误消息。  
  
## <a name="syntax"></a>语法  
  
```  
  
Error( [ Error_Text ] )  
```  
  
## <a name="arguments"></a>参数  
 *Error_Text*  
 包含要返回的错误消息的有效字符串表达式。  
  
## <a name="examples"></a>示例  
 以下查询说明如何使用**错误**内计算度量值的函数：  
  
 `WITH MEMBER MEASURES.ERRORDEMO AS ERROR("THIS IS AN ERROR")`  
  
 `SELECT`  
  
 `MEASURES.ERRORDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
