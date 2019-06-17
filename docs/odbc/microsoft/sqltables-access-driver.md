---
title: SQLTables （Access 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Access Driver
- Access driver [ODBC], SQLTables
ms.assetid: 94423cf9-341a-4db6-bb10-8f5448df7fc3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9931d3d02ff2d0afe69f410d94474c16f235b94e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62686821"
---
# <a name="sqltables-access-driver"></a>SQLTables（Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|参数|注释|  
|--------------|--------------|  
|*szTableOwner*|唯一有效参数*szTableOwner*为 NULL，因为没有任何驱动程序支持所有者名称。 与*szTableOwner*设置为 NULL，则返回所有表。 在 TABLE_OWNER 列中返回 NULL。|  
|*szTableQualifier*|在 TABLE_QUALIFIER 专栏中， **SQLTables**将返回数据库文件的路径。|  
|*SzTableType*|使用 Microsoft Access 驱动程序时，支持"系统表" *szTableType*系统表中，对于"同义词"支持的附加表和"视图"支持的返回行的查询。|  
  
## <a name="see-also"></a>请参阅  
 [SQLTables 函数](../../odbc/reference/syntax/sqltables-function.md)
