---
title: CustomData （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d2884e23cbee78acacdb72e386f0e99610e9629f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135826"
---
# <a name="customdata-mdx"></a>CustomData (MDX)


  如果已定义，则返回**CustomData**连接字符串属性的值;否则**为 null**。  
  
## <a name="syntax"></a>语法  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>返回值  
 **CustomData**函数可以检索**CustomData**连接字符串属性，并传递由多维表达式（mdx）函数和语句（如[UserName （mdx）](../mdx/username-mdx.md)和[CALL 语句（mdx））](../mdx/mdx-data-manipulation-call.md)使用的配置设置。 例如，可以在动态安全表达式中使用此函数，为**CustomData**连接字符串属性中的字符串值选择允许/拒绝的集成员。  
  
## <a name="example"></a>示例  
 下面的查询在计算度量值中显示**CustomData**函数返回的值：  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
