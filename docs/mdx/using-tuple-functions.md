---
title: "使用元组函数 |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: tuple functions
ms.assetid: fe41e3e5-a675-4169-a966-b42c18e8d741
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4fdb557918f60f19eef47b79796e6f1f49ff1316
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="using-tuple-functions"></a>使用元组函数
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  元组函数从集中检索元组，或者通过解析元组的字符串表示形式来检索元组。  
  
 与成员函数和集函数一样，元组函数对协商 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中的多维结构至关重要。  
  
 在 MDX 中，有三个元组函数[当前 &#40;MDX &#41;](../mdx/current-mdx.md)，[项 &#40;元组 &#41;&#40;MDX &#41;](../mdx/item-tuple-mdx.md)和[StrToTuple &#40;MDX &#41;](../mdx/strtotuple-mdx.md). 以下示例查询说明如何使用这三个函数：  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of Years and Countries`  
  
 `SET MyTuples AS  [Date].[Calendar Year].[Calendar Year].MEMBERS * [Customer].[Country].[Country].MEMBERS`  
  
 `//Returns a string representation of that set using the Current and Generate functions`  
  
 `MEMBER MEASURES.CURRENTDEMO AS GENERATE(MyTuples, TUPLETOSTR(MyTuples.CURRENT), ", ")`  
  
 `//Retrieves the fourth tuple from that set and displays it as a string`  
  
 `MEMBER MEASURES.ITEMDEMO AS TUPLETOSTR(MyTuples.ITEM(3))`  
  
 `//Creates a tuple consisting of the measure Internet Sales Amount and the country Australia from a string`  
  
 `MEMBER MEASURES.STRTOTUPLEDEMO AS STRTOTUPLE("([Measures].[Internet Sales Amount]" + ", [Customer].[Country].&[Australia])")`  
  
 `SELECT{MEASURES.CURRENTDEMO,MEASURES.ITEMDEMO,MEASURES.STRTOTUPLEDEMO} ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [函数 &#40;MDX 语法 &#41;](../mdx/functions-mdx-syntax.md)   
 [使用成员函数](../mdx/using-member-functions.md)   
 [使用集函数](../mdx/using-set-functions.md)  
  
  
