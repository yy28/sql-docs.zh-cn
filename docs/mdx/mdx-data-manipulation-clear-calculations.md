---
description: MDX 数据操作 - CLEAR CALCULATIONS
title: 清除计算语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 06f3fc9d29630f3f69b994c2b4e7cf809b6b9efd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387001"
---
# <a name="mdx-data-manipulation---clear-calculations"></a>MDX 数据操作 - CLEAR CALCULATIONS


  从多维数据集中删除所有计算，并将多维数据集恢复为计算传递 0。  
  
## <a name="syntax"></a>语法  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>参数  
 *Cube_Expression*  
 有效的多维表达式 (MDX) 多维数据集表达式。  
  
## <a name="remarks"></a>备注  
 当多维数据集的上下文已知时，可以省略 **FROM** 子句，例如在 MDX 脚本中。  
  
> [!NOTE]  
>  只有服务器管理员、数据库管理员或具有多维数据集中源数据访问权（即 ReadSourceData=true）的角色的成员才能执行此语句。  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 数据操作语句 &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
