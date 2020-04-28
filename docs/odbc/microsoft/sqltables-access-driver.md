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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df3a23af365efbef6a0f0da2c52568501425ecb3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306088"
---
# <a name="sqltables-access-driver"></a>SQLTables（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
|参数|说明|  
|--------------|--------------|  
|*szTableOwner*|*SzTableOwner*的唯一有效参数是 NULL，因为这些驱动程序都不支持所有者名称。 如果*szTableOwner*设置为 NULL，则返回所有表。 在 TABLE_OWNER 列中返回 NULL。|  
|*szTableQualifier*|在 TABLE_QUALIFIER 列中， **SQLTables**将返回数据库文件的路径。|  
|*SzTableType*|使用 Microsoft Access 驱动程序时，系统表的*szTableType*支持 "系统表"，附加表支持 "同义词"，行返回查询支持 "视图"。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLTables 函数](../../odbc/reference/syntax/sqltables-function.md)
