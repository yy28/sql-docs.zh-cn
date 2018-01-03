---
title: "SQLTables （Paradox 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Paradox driver [ODBC], SQLTables
- SQLTables function [ODBC], Paradox Driver
ms.assetid: d68adad6-97bd-4b47-bcf9-0102aafb00d4
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b11865bc59b2fbdbc81a771fadd099dde78f1f42
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqltables-paradox-driver"></a>SQLTables （Paradox 驱动程序）
> [!NOTE]  
>  本主题提供 Paradox 特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|参数|注释|  
|--------------|--------------|  
|*szTableOwner*|唯一有效参数*szTableOwner*是 NULL，因为无驱动程序支持所有者名称。 与*szTableOwner*设置为 NULL，返回所有表。 TABLE_OWNER 列中返回 NULL。|  
|*szTableQualifier*|在 TABLE_QUALIFIER 列中， **SQLTables**将返回目录的路径。|  
|*SzTableType*|对于 Paradox 文件，"表"是唯一支持的表类型。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLTables 函数](../../odbc/reference/syntax/sqltables-function.md)
