---
title: 表名称 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303118"
---
# <a name="table-names"></a>表名称
当使用 dBASE、Microsoft Excel、Paradox 或文本驱动程序时，在"选择"或"删除"的 FROM 子句中、INSERT 中的 INTO 子句之后以及更新后、创建表和 DROP TABLE 中发生的表名称可以包含有效的路径、主名称和文件名扩展名。  
  
 在 SQL 语句的其他位置使用表名称不支持使用路径或扩展，但仅接受主名称（例如，EMP FROM FROM C：\ABC_EMP）。  
  
 可以使用关联名称（别名）。 例如：  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
