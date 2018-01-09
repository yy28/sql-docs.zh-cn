---
title: "删除 SET 语句 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET
- DROP
- DROP SET
- DROP_SET
dev_langs: kbMDX
helpviewer_keywords:
- DROP SET statement
- deleting named sets
- named sets [MDX]
- removing named sets
- dropping named sets
ms.assetid: bbc37afb-af8c-41df-ba81-12771beb1c41
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 72c0c0816e250f135790604c2c832b87d74c0be2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-definition---drop-set"></a>MDX 数据定义-删除组
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  删除一个命名集。  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP [SESSION] SET   
   <Cube_Reference>.Set_Name   
               [,<Cube_Reference>.Set_Name ...n]  
  
<Cube_Reference> ::= {CURRENTCUBE | Cube_Name}  
  
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 有效的字符串表达式，它提供的多维数据集的名称。  
  
 *Set_Name*  
 有效字符串表达式，提供将要删除的命名集的名称。  
  
## <a name="remarks"></a>Remarks  
 有关命名集的详细信息，请参阅[在 MDX 中生成命名集 (MDX)](../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md)。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 数据定义语句 &#40;MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
