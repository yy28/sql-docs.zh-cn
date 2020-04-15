---
title: SQLTables（访问驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df3a23af365efbef6a0f0da2c52568501425ecb3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306088"
---
# <a name="sqltables-access-driver"></a>SQLTables（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
|参数|注释|  
|--------------|--------------|  
|*szTable 所有者*|*szTableOwner*的唯一有效参数是 NULL，因为没有任何驱动程序支持所有者名称。 将*szTableOwner*设置为 NULL 时，将返回所有表。 NULL 在TABLE_OWNER列中返回。|  
|*szTable限定符*|在TABLE_QUALIFIER列中 **，SQLTables**将路径返回到数据库文件。|  
|*SzTable 类型*|使用 Microsoft 访问驱动程序时，系统表的*szTableType*支持"SYSTEM TABLE"，附加表支持"SYNONYM"，对于返回行的查询支持"VIEW"。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLTables 函数](../../odbc/reference/syntax/sqltables-function.md)
