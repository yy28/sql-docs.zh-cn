---
description: Error (MDX)
title: MDX)  (错误 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f95ee71586f5571d91221fe8889198a44a1252b3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494920"
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
 下面的查询显示了如何在计算度量值中使用 **Error** 函数：  
  
 `WITH MEMBER MEASURES.ERRORDEMO AS ERROR("THIS IS AN ERROR")`  
  
 `SELECT`  
  
 `MEASURES.ERRORDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
