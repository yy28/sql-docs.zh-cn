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
manager: craigg
ms.openlocfilehash: 2d72d7868d0e19719ea7992bdb8ccd1f61f3718d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755727"
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
