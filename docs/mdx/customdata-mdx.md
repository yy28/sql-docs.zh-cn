---
title: CustomData (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 172915d99b231490cbdca24f70d1d38da27a1d3d
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739298"
---
# <a name="customdata-mdx"></a>CustomData (MDX)


  返回的值**CustomData**连接字符串属性定义; 否则为如果**null**。  
  
## <a name="syntax"></a>语法  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>返回值  
 **CustomData**函数可检索**CustomData**连接字符串属性，并将传递的配置设置以由多维表达式 (MDX) 函数和语句，如使用[用户名 (MDX)](../mdx/username-mdx.md)和[调用语句 (MDX)](../mdx/mdx-data-manipulation-call.md)。 例如，此函数可以使用动态安全性表达式中，若要选择的字符串值中的允许/拒绝集成员**CustomData**连接字符串属性。  
  
## <a name="example"></a>示例  
 下面的查询显示返回的值**CustomData**中计算的度量值的函数：  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
