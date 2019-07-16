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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939790"
---
# <a name="table-names"></a>表名称
DBASE、 Microsoft Excel、 Paradox，或使用驱动程序的文本、 表名中发生的 FROM 子句的 SELECT 或 DELETE 之后在 INSERT INTO 子句, 和更新后，CREATE TABLE 和 DROP TABLE 可以包含有效的路径、 主名称和文件名称扩展时.  
  
 使用 SQL 语句中的其他位置的表名不支持的路径或扩展插件使用，但将接受主名称 (例如，EMP 从 C:\ABC\EMP)。  
  
 可以使用相关名称 （别名）。 例如：  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
