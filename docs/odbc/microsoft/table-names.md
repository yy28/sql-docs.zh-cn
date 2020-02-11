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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5dd8de055521f4a1831d20a9a34bedb9309d1de6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67939790"
---
# <a name="table-names"></a>表名称
当使用 dBASE、Microsoft Excel、Paradox 或文本驱动程序时，在 SELECT 或 DELETE 的 FROM 子句中出现的表名，在 UPDATE、CREATE TABLE 和 DROP 表后，它们可以包含有效路径、主名称和文件扩展名.  
  
 如果在 SQL 语句中的其他位置使用表名称，则不支持使用路径或扩展名，只接受主名称（例如，C:\ABC\EMP 中的 EMP）。  
  
 可以使用相关名称（别名）。 例如：  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
