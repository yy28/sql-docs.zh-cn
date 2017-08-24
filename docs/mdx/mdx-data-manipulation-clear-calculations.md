---
title: "清除计算语句 (MDX) |Microsoft 文档"
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
- CLEAR CALCULATIONS
- clalculations
- clear
dev_langs:
- kbMDX
helpviewer_keywords:
- clearing calculations
- CLEAR CALCULATIONS statement
- deleting calculations
- removing calculations
- calculations [Analysis Services], clearing
- cubes [Analysis Services], calculations
ms.assetid: aebec9a1-1d1d-4697-aa3f-cc2449625603
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 042c7b9bedc396d63aa70d23926728b015527a99
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-manipulation---clear-calculations"></a>MDX 数据操作-清除计算
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从多维数据集中删除所有计算，并将多维数据集恢复为计算传递 0。  
  
## <a name="syntax"></a>语法  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>参数  
 *Cube_Expression*  
 有效的多维表达式 (MDX) 多维数据集表达式。  
  
## <a name="remarks"></a>備註  
 **FROM**已知，如所 MDX 脚本的多维数据集的上下文时，可以省略子句。  
  
> [!NOTE]  
>  只有服务器管理员、数据库管理员或具有多维数据集中源数据访问权（即 ReadSourceData=true）的角色的成员才能执行此语句。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 数据操作语句 &#40;MDX &#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  

