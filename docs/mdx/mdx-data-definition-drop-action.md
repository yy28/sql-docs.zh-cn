---
title: "删除操作语句 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP
- DROP ACTION
- Action
- DROP_ACTION
dev_langs:
- kbMDX
helpviewer_keywords:
- DROP ACTION statement
- deleting actions
- removing actions
- actions [MDX]
- dropping actions
ms.assetid: 74b3cfee-dea8-4968-a54c-1754d52ee1bd
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 99866db174208e4d041e69cae3d3b520eefb8dba
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---drop-action"></a>MDX 数据定义-删除操作
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从指定多维数据集中删除指定的操作。  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP ACTION CURRENTCUBE | Cube_Name  
   .Action_Name   
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 有效的字符串表达式，它提供多维数据集名称。  
  
 *Action_Name*  
 提供要删除操作的名称的有效字符串表达式。  
  
## <a name="see-also"></a>另请参阅  
 [创建操作语句 &#40;MDX &#41;](../mdx/mdx-data-definition-create-action.md)   
 [MDX 数据定义语句 &#40;MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

