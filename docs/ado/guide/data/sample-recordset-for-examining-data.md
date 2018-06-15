---
title: 记录集的示例性检查的数据 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a6bb3eb784c3979dd136f237c5d153547d30027
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272486"
---
# <a name="sample-recordset-for-examining-data"></a>示例以检查数据的记录集
首先，让我们看一下**记录集**对象，如使用以下 SQL 查询中，执行针对 Microsoft SQL Server 中的基的 Northwind 示例数据返回。  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 所产生的**记录集**对象包含下表中所示的数据库中的所有生成。  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|位置 Bob 环保干的梨|30.0000|  
|14|豆腐|23.2500|  
|28|Rssle 泡菜口味|45.6000|  
|51|猪肉干|53.0000|  
|74|Longlife 豆腐|10.0000|  
  
 如果你有兴趣自行获取这些结果，请尝试以下 JScript 示例：  
  
-   [JScript 示例返回一个记录集](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
