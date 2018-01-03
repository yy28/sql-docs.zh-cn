---
title: "SQLTables （Access 驱动程序） |Microsoft 文档"
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
- SQLTables function [ODBC], Access Driver
- Access driver [ODBC], SQLTables
ms.assetid: 94423cf9-341a-4db6-bb10-8f5448df7fc3
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 895c4d86c11d88fcf544b9a3c7612e1a6cdf4764
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqltables-access-driver"></a>SQLTables （Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|参数|注释|  
|--------------|--------------|  
|*szTableOwner*|唯一有效参数*szTableOwner*是 NULL，因为无驱动程序支持所有者名称。 与*szTableOwner*设置为 NULL，返回所有表。 TABLE_OWNER 列中返回 NULL。|  
|*szTableQualifier*|在 TABLE_QUALIFIER 列中， **SQLTables**将返回数据库文件的路径。|  
|*SzTableType*|当使用 Microsoft Access 驱动程序时，支持"系统表" *szTableType*对于系统表，"同义词"附加表和支持"视图"支持的返回行的查询。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLTables 函数](../../odbc/reference/syntax/sqltables-function.md)
