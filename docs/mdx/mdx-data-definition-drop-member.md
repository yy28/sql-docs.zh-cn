---
title: DROP MEMBER 语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 78d5d27853922d7e7524d93ae2b8157e57166968
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248302"
---
# <a name="mdx-data-definition---drop-member"></a>MDX 数据定义 - DROP MEMBER


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
 提供成员名称或成员键的有效字符串表达式。  
  
## <a name="see-also"></a>请参阅  
 [CREATE MEMBER 语句 (MDX)](../mdx/mdx-data-definition-create-member.md)   
 [MDX 数据定义语句&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
