---
title: "数据成员 (MDX) |Microsoft 文档"
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
- DATAMEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- DataMember function
ms.assetid: 65bf21e8-1cb2-4ae8-bfbe-bb4d72589557
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b6be9e31f666eafaba1ec7ad346a7e5bb28da9b0
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="datamember-mdx"></a>DataMember (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回系统生成的、与某个维度的非叶成员相关联的数据成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 此函数对任何层次结构中的非叶成员进行操作，并可由[更新多维数据集语句 (MDX)](../mdx/mdx-data-manipulation-update-cube.md)命令到非叶成员直接，而不是叶成员的后代的写回数据。  
  
> [!NOTE]  
>  如果指定的成员为叶成员，或者如果非叶成员没有关联的数据成员，则返回指定的成员。  
  
## <a name="example"></a>示例  
 下面的示例使用**DataMember**中计算的度量值，以显示每个单个员工的销售定额函数：  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX &#40; 中的重要概念Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  

