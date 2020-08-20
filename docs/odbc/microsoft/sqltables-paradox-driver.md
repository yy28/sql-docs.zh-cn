---
description: SQLTables（Paradox 驱动程序）
title: SQLTables (Paradox 驱动程序) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLTables
- SQLTables function [ODBC], Paradox Driver
ms.assetid: d68adad6-97bd-4b47-bcf9-0102aafb00d4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5da80e16a63431bd7a0ddf46c2efaa236ecefd3e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500130"
---
# <a name="sqltables-paradox-driver"></a>SQLTables（Paradox 驱动程序）
> [!NOTE]  
>  本主题提供了特定于驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
|参数|注释|  
|--------------|--------------|  
|*szTableOwner*|*SzTableOwner*的唯一有效参数是 NULL，因为这些驱动程序都不支持所有者名称。 如果 *szTableOwner* 设置为 NULL，则返回所有表。 在 TABLE_OWNER 列中返回 NULL。|  
|*szTableQualifier*|在 TABLE_QUALIFIER 列中， **SQLTables** 将返回目录的路径。|  
|*SzTableType*|对于 Paradox 文件，"表" 是唯一支持的表类型。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLTables 函数](../../odbc/reference/syntax/sqltables-function.md)
