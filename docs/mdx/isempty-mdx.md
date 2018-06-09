---
title: IsEmpty (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dbed0eba3fec73d7134b1ce21275c28dbd387fcd
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740166"
---
# <a name="isempty-mdx"></a>IsEmpty (MDX)


  返回表达式的计算结果是否为空单元值。  
  
## <a name="syntax"></a>语法  
  
```  
  
IsEmpty(Value_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Value_Expression*  
 有效 MDX（多维表达式）表达式，通常返回成员或元组的单元坐标。  
  
## <a name="remarks"></a>Remarks  
 **IsEmpty**函数返回**true**如果计算的表达式是空单元值。 否则，此函数返回**false**。  
  
> [!NOTE]  
>  成员的默认属性为成员的值。  
  
 **IsEmpty**函数是唯一的方法来可靠地测试空单元格，因为空单元值在中具有特殊含义[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
> [!IMPORTANT]  
>  如果值表达式的计算结果将返回错误，则该函数将返回**false**。 值表达式也可能返回错误，例如，属性引用引用了无效或不存在的属性。  
  
 有关空单元的详细信息，请参阅 OLE DB 文档。  
  
## <a name="example"></a>示例  
 如果 Date 维度的 Fiscal 层次结构上当前成员的 Internet Sales Amount 返回一个空单元，则下面的示例将返回 TRUE：  
  
 `WITH MEMBER MEASURES.ISEMPTYDEMO AS`  
  
 `IsEmpty([Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.ISEMPTYDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [使用空值](../mdx/working-with-empty-values.md)   
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
