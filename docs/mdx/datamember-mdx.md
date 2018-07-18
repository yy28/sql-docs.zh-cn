---
title: 数据成员 (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98b10c951043416280c05fd6a0e5eeb5df92c104
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739486"
---
# <a name="datamember-mdx"></a>DataMember (MDX)


  返回系统生成的、与某个维度的非叶成员相关联的数据成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 中的重要概念&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  
