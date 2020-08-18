---
description: CustomData (MDX)
title: CustomData (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ed7bfe2841caf9bd5b2c6e6caf102323db6d62ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413163"
---
# <a name="customdata-mdx"></a>CustomData (MDX)


  如果已定义，则返回 **CustomData** 连接字符串属性的值;否则 **为 null**。  
  
## <a name="syntax"></a>语法  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>返回值  
 **CustomData**函数可以检索**CustomData**连接字符串属性，并传递一个配置设置，该设置由 (mdx) 函数和语句的多维表达式（如[用户名 (mdx) ](../mdx/username-mdx.md)和[CALL 语句 (mdx) ](../mdx/mdx-data-manipulation-call.md)）使用。 例如，可以在动态安全表达式中使用此函数，为 **CustomData** 连接字符串属性中的字符串值选择允许/拒绝的集成员。  
  
## <a name="example"></a>示例  
 下面的查询在计算度量值中显示 **CustomData** 函数返回的值：  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
