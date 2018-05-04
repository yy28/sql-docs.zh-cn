---
title: CustomData (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- EXISTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Exists function
ms.assetid: 61d9f5a2-6f56-4179-a39b-317c8e0a2cdd
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5fb7c745ac65b41095c3d4dfb41b62b081d83c1d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="customdata-mdx"></a>CustomData (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
