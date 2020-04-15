---
title: SQLTables（悖论驱动程序） |微软文档
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
ms.openlocfilehash: aa13b5395d8f3c2cb470a4eff1b1ef02a43bad53
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299280"
---
# <a name="sqltables-paradox-driver"></a>SQLTables（Paradox 驱动程序）
> [!NOTE]  
>  本主题提供特定于悖论驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
|参数|注释|  
|--------------|--------------|  
|*szTable 所有者*|*szTableOwner*的唯一有效参数是 NULL，因为没有任何驱动程序支持所有者名称。 将*szTableOwner*设置为 NULL 时，将返回所有表。 NULL 在TABLE_OWNER列中返回。|  
|*szTable限定符*|在TABLE_QUALIFIER列中 **，SQLTables**将路径返回到目录。|  
|*SzTable 类型*|对于 Paradox 文件，"TABLE"是唯一支持的表类型。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLTables 函数](../../odbc/reference/syntax/sqltables-function.md)
