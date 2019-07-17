---
title: CustomData (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d2884e23cbee78acacdb72e386f0e99610e9629f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135826"
---
# <a name="customdata-mdx"></a>CustomData (MDX)


  返回的值**CustomData**连接字符串属性，如果定义; 否则为**null**。  
  
## <a name="syntax"></a>语法  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>返回值  
 **CustomData**函数可检索**CustomData**连接字符串属性，并传递的配置设置以使用由多维表达式 (MDX) 函数和语句，如[UserName (MDX)](../mdx/username-mdx.md)并[CALL 语句 (MDX)](../mdx/mdx-data-manipulation-call.md)。 例如，此函数可以使用动态安全表达式中，选择中的字符串值的允许或拒绝的集成员**CustomData**连接字符串属性。  
  
## <a name="example"></a>示例  
 以下查询显示返回的值**CustomData**中计算的度量值的函数：  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
