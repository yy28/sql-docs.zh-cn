---
title: 选择与值不匹配的行 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], rows not matching value
- row not matching value [SQL Server]
- NOT operator [Visual Database Tools]
- search criteria [SQL Server], rows not matching value
ms.assetid: 19898578-7b2f-401c-bb8f-9f2a017efdf7
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aa3084d9b624f1836a3970da77c01677b7700ba4
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43814283"
---
# <a name="select-rows-that-do-not-match-a-value-visual-database-tools"></a>选择与值不匹配的行 (Visual Database Tools)
  若要查找与某值不匹配的行，可以使用 NOT 运算符。  
  
### <a name="to-find-rows-that-do-not-match-a-value"></a>查找与某值不匹配的行  
  
1.  如果尚未指定搜索条件，请将要在搜索条件内使用的列或表达式添加到[“条件”窗格](visual-database-tools.md)中。  
  
2.  找到包含要搜索的数据列或表达式的行，然后在“筛选器”网格列中，顺序输入 NOT 运算符和搜索值。  
  
 例如，若要在 `products` 表中查找产品代码列中的值以“A”之外的其他字符开头的所有行，则可以输入如下搜索条件：  
  
```  
NOT LIKE 'A%'  
```  
  
## <a name="see-also"></a>请参阅  
 [输入规则搜索值&#40;可视化数据库工具&#41;](rules-for-entering-search-values-visual-database-tools.md)   
 [指定搜索条件 (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)  
  
  
