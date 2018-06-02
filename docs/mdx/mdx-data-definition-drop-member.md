---
title: 删除成员语句 (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5de7a54dd7b6b6ac35a44639c04cc1072117de7b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579579"
---
# <a name="mdx-data-definition---drop-member"></a>MDX 数据定义-删除成员
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  删除一个计算成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP MEMBER   
   CURRENTCUBE | Cube_Name  
      .Member_Name   
               [,CURRENTCUBE | Cube_Name.Member_Name ...n]  
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 提供多维数据集名称的有效字符串表达式。  
  
 *Member_Identifier*  
 有效的字符串表达式，它提供的成员名称或成员键。  
  
## <a name="see-also"></a>请参阅  
 [创建成员语句&#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [MDX 数据定义语句&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
