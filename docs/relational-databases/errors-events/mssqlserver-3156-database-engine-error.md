---
title: MSSQLSERVER_3156 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3156 (Database Engine error)
ms.assetid: 345d8ed4-177e-4ec3-bab3-25d30000e323
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 98be55981545c010307eff9368af5dc39cf1b1f2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver3156"></a>MSSQLSERVER_3156
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|3156|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LDDB_CANT_WRITE|  
|消息正文|文件 '%ls' 无法还原为 '%ls'。 请使用 WITH MOVE 选项来标识该文件的有效位置。|  
  
## <a name="explanation"></a>解释  
此常规消息标识因指定位置错误而无法还原的文件的逻辑文件名或物理文件名。  
  
### <a name="possible-causes"></a>可能的原因  
可能的原因包括：  
  
-   可能需要具备对指定 Windows 目录的访问权限。  
  
-   键入的路径可能有误或指定的路径不存在。  
  
-   某个无法覆盖的文件可能正在使用该文件名。  
  
## <a name="user-action"></a>用户操作  
在错误日志中查找提供详细信息的其他消息。  
  
更正指定位置的错误，例如，授予访问权限或使用 RESTORE 语句中的 WITH MOVE 选项重新定位文件。  
  
## <a name="see-also"></a>另请参阅  
[将数据库还原到新位置 (SQL Server)](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[将文件还原到新位置 (SQL Server)](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  
