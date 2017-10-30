---
title: MSSQLSERVER_5242 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 5242 (Database Engine error)
ms.assetid: 712b1a10-2f87-41df-a111-1ed9f14102d4
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c0cbd395e12518d755d9fc35026efadb872ba5c0
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver5242"></a>MSSQLSERVER_5242
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|5242|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|在数据库 '%.*ls'(ID:%d) 中对页 %S_PGID 执行内部操作期间检测到不一致性。 请与技术支持联系。 参考号为 %ld。|  
  
## <a name="explanation"></a>解释  
在错误消息中引用的数据库页上出现结构不一致性。  
  
## <a name="see-also"></a>另请参阅  
[DBCC CHECKDB (Transact-SQL)](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[数据库文件和文件组](~/relational-databases/databases/database-files-and-filegroups.md)  
  

