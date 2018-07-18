---
title: 清除计算语句 (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cdc4b2d3e948f0123eb15e38a6140e63009907bc
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742386"
---
# <a name="mdx-data-manipulation---clear-calculations"></a>MDX 数据操作-清除计算


  从多维数据集中删除所有计算，并将多维数据集恢复为计算传递 0。  
  
## <a name="syntax"></a>语法  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>参数  
 *Cube_Expression*  
 有效的多维表达式 (MDX) 多维数据集表达式。  
  
## <a name="remarks"></a>Remarks  
 **FROM**已知，如所 MDX 脚本的多维数据集的上下文时，可以省略子句。  
  
> [!NOTE]  
>  只有服务器管理员、数据库管理员或具有多维数据集中源数据访问权（即 ReadSourceData=true）的角色的成员才能执行此语句。  
  
## <a name="see-also"></a>请参阅  
 [MDX 数据操作语句&#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
