---
title: DROP ACTION 语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f47eaad9a13966abd1d08b0121fdd9c0a64a7438
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63285061"
---
# <a name="mdx-data-definition---drop-action"></a>MDX 数据定义 - DROP ACTION


  从指定多维数据集中删除指定的操作。  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP ACTION CURRENTCUBE | Cube_Name  
   .Action_Name   
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 提供多维数据集名称的有效字符串表达式。  
  
 *Action_Name*  
 提供要删除操作的名称的有效字符串表达式。  
  
## <a name="see-also"></a>请参阅  
 [CREATE ACTION 语句&#40;MDX&#41;](../mdx/mdx-data-definition-create-action.md)   
 [MDX 数据定义语句&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
