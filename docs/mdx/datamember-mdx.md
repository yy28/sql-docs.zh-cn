---
title: DataMember （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4395f0ff113c8549ec2250d5fa87d37090627b3c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892915"
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
  
## <a name="remarks"></a>备注  
 此函数对任何层次结构中的非叶成员进行操作，并且可由[UPDATE CUBE 语句（MDX）](../mdx/mdx-data-manipulation-update-cube.md)命令用来将数据直接写回非叶成员的后代，而不是与叶成员的后代一起使用。  
  
> [!NOTE]  
>  如果指定的成员为叶成员，或者如果非叶成员没有关联的数据成员，则返回指定的成员。  
  
## <a name="example"></a>示例  
 下面的示例在计算度量值中使用**DataMember**函数显示每个雇员的销售配额：  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX &#40;Analysis Services 中的关键概念&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)  
  
  
