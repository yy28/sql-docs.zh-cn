---
title: 用于检查数据的示例记录集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9ffc34dd95ac2f5ef6e26e796c4c05cd91b28ae0
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700396"
---
# <a name="sample-recordset-for-examining-data"></a>用于检查数据的示例记录集
首先，让我们看看**记录集**对象返回使用以下 SQL 查询，执行针对 Microsoft SQL Server 中的基的 Northwind 示例数据。  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 所产生的**记录集**对象包含下表中所示在数据库中的所有生成。  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|柳贡干的梨|30.0000|  
|14|豆腐|23.2500|  
|28|Rssle Sauerkraut|45.6000|  
|51|猪肉干|53.0000|  
|74|Longlife 豆腐|10.0000|  
  
 如果您有兴趣自行获取这些结果，请尝试以下 JScript 示例：  
  
-   [若要返回记录集的 JScript 示例](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
