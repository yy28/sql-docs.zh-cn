---
title: MSSQLSERVER_2530 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: 5d4be07a-38a5-4b25-819c-4dcb4636cc15
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1bb321f89c70983855e00b3eec4382c51fce1e16
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552046"
---
# <a name="mssqlserver_2530"></a>MSSQLSERVER_2530
    
## <a name="details"></a>详细信息  
  
|Attribute|值|  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2530|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_INDEX_IS_OFFLINE|  
|消息正文|表 "%.\*ls" 的索引 "%.*ls" 已禁用。|  
  
## <a name="explanation"></a>说明  
 DBCC 语句无法继续，因为指定的索引已禁用。 索引被禁用后一直保持禁用状态，直到它重新生成或删除并重新创建。  
  
## <a name="user-action"></a>用户操作  
  
1.  可以通过使用下列方法之一来启用已禁用的索引：  
  
    -   带 REBUILD 子句的 ALTER INDEX 语句  
  
    -   带 DROP_EXISTING 子句的 CREATE INDEX  
  
    -   DBCC DBREINDEX  
  
2.  请重新运行 DBCC 语句。  
  
## <a name="see-also"></a>另请参阅  
 [启用索引和约束](../indexes/enable-indexes-and-constraints.md)   
 [ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql)   
 [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql)   
 [DBCC DBREINDEX (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql)  
  
  
