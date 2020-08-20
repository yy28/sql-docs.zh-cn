---
description: 表名称
title: 表名 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b264999f800e4387099240526f558110c39e27a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471455"
---
# <a name="table-names"></a>表名称
当使用 dBASE、Microsoft Excel、Paradox 或 Text 驱动程序时，在 SELECT 或 DELETE 的 FROM 子句中出现的表名，在 UPDATE、CREATE TABLE 和 DROP 表后，它们可以包含有效路径、主名称和文件扩展名。  
  
 如果在 SQL 语句中的其他位置使用表名称，则不支持使用路径或扩展名，只接受主名称 (例如，EMP 从 C:\ABC\EMP) 。  
  
 可以使用 (别名) 相关名称。 例如：  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
