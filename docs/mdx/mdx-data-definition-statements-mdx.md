---
title: "MDX 数据定义语句 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- MDX [Analysis Services], data manipulation
- data manipulation [MDX]
- data definition statements [MDX]
- Multidimensional Expressions [Analysis Services], data manipulation
ms.assetid: 1f975d7f-8875-43b6-a571-9d5cd7c70217
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7799b80fd5ba847492247f1d52107da4aaf569a1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition-statements-mdx"></a>MDX 数据定义语句 (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在多维表达式 (MDX) 中，数据定义语句可以创建、删除和操作多维对象。 下表列出了可用的数据定义语句。  
  
## <a name="in-this-section"></a>本節內容  
  
|主题|Description|  
|-----------|-----------------|  
|[ALTER CUBE 语句 &#40;MDX &#41;](../mdx/mdx-data-definition-alter-cube.md)|更改指定多维数据集的结构。|  
|[创建操作语句 &#40;MDX &#41;](../mdx/mdx-data-definition-create-action.md)|创建可以与多维数据集、维度、层次结构或从属对象关联的操作。|  
|[创建单元格计算语句 &#40;MDX &#41;](../mdx/mdx-data-definition-create-cell-calculation.md)|创建计算，以便对多维数据集内一组指定的元组进行 MDX 表达式求值。|  
|[创建全局多维数据集语句 &#40;MDX &#41;](../mdx/mdx-data-definition-create-global-cube.md)|基于服务器上某个多维数据集中的子多维数据集，创建并填充一个本地持久化多维数据集。 不需要连接到服务器就可以连接到本地持久化多维数据集。|  
|[创建成员语句 &#40;MDX &#41;](../mdx/mdx-data-definition-create-member.md)|创建计算成员。|  
|[创建会话多维数据集语句 &#40;MDX &#41;](../mdx/mdx-data-definition-create-session-cube.md)|基于服务器上的多维数据集，创建并填充对同一会话中的所有查询均可用的多维数据集。|  
|[创建 SET 语句 &#40;MDX &#41;](../mdx/mdx-data-definition-create-set.md)|为指定的多维数据集创建命名集。|  
|[创建子多维数据集语句 &#40;MDX &#41;](../mdx/mdx-data-definition-create-subcube.md)|将所指定多维数据集或子多维数据集的多维数据集空间重定义给一个指定的子多维数据集。|  
|[DROP 操作语句 &#40;MDX &#41;](../mdx/mdx-data-definition-drop-action.md)|从指定多维数据集中删除指定的操作。|  
|[DROP 单元格计算语句 &#40;MDX &#41;](../mdx/mdx-data-definition-drop-cell-calculation.md)|删除指定的单元计算。|  
|[DROP 成员语句 &#40;MDX &#41;](../mdx/mdx-data-definition-drop-member.md)|删除一个计算成员。|  
|[删除 SET 语句 &#40;MDX &#41;](../mdx/mdx-data-definition-drop-set.md)|删除一个命名集。|  
|[DROP SUBCUBE 语句 &#40;MDX &#41;](../mdx/mdx-data-definition-drop-subcube.md)|删除指定的子多维数据集，以恢复到以前定义的具有指定名称的多维数据集或子多维数据集定义。|  
|[刷新多维数据集语句 &#40;MDX &#41;](../mdx/mdx-data-definition-refresh-cube.md)|刷新多维数据集的客户端缓存。|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 语句引用 &#40;MDX &#41;](../mdx/mdx-statement-reference-mdx.md)   
 [MDX 数据操作语句 &#40;MDX &#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [MDX 脚本语句 &#40;MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  

