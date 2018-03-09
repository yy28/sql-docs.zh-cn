---
title: "记录集的示例性检查的数据 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66ed865b10da98f63c087cc56191300e058403c3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
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
