---
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
ms.openlocfilehash: 91a415cd456186f18ef358b9d504145f78152774
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303118"
---
# <a name="table-names"></a>表名称
当使用 dBASE、Microsoft Excel、Paradox 或 Text 驱动程序时，在 SELECT 或 DELETE 的 FROM 子句中出现的表名，在 UPDATE、CREATE TABLE 和 DROP 表后，它们可以包含有效路径、主名称和文件扩展名。  
  
 如果在 SQL 语句中的其他位置使用表名称，则不支持使用路径或扩展名，只接受主名称（例如，C:\ABC\EMP 中的 EMP）。  
  
 可以使用相关名称（别名）。 例如：  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
