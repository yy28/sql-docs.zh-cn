---
title: MSSQLSERVER_3456 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 3456 (Database Engine error)
ms.assetid: d11b2b2c-3ae4-4023-b82f-05b561bfacce
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3e32ff570075317df72fc6a4c0f579c79f0d78b4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015693"
---
# <a name="mssqlserver3456"></a>MSSQLSERVER_3456
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3456|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|REC_REDOLSNMISMATCH|  
|消息正文|对于事务 ID %S_XID，无法在数据库 '%.*ls' (数据库 ID 为 %d)的页 %S_PGID 上重做日志记录 %S_LSN。 页: LSN = %S_LSN，类型 = %ld。 日志: 操作码 = %ld，上下文 %ld，上一页的 LSN: %S_LSN。 请从数据库备份还原该数据库，或者修复它。|  
  
## <a name="explanation"></a>解释  
 还原操作无法重做事务日志。 此错误使数据库进入 SUSPECT 状态。 主文件组以及可能其他文件组可疑并可能受损。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动过程中无法恢复数据库，因此无法使用该数据库。 需要用户执行操作来解决问题。  
  
 请注意，如果对于 **tempdb**发生此错误，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例关闭。  
  
## <a name="user-action"></a>用户操作  
 此错误可能是由在某次尝试启动服务器实例或恢复数据库的过程中系统上存在的暂时性条件导致的。 此错误也可能是由当您每次尝试启动数据库时发生的永久性错误导致的。 有关原因的信息，请检查 Windows 事件日志以了解有关指示特定故障的先前错误。  
  
 有关错误 3456 出现原因的信息，请检查 Windows 事件日志以了解有关指示特定故障的先前错误。 相应的用户操作取决于 Windows 事件日志中的信息是否指示该 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误由暂时条件或永久性故障导致。 有关排除 3456 错误的用户操作的信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书。  
  
## <a name="see-also"></a>请参阅  
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)   
 [DBCC CHECKDB (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [完整数据库还原（简单恢复模式）](../backup-restore/complete-database-restores-simple-recovery-model.md)   
 [MSSQLSERVER_824](mssqlserver-824-database-engine-error.md)   
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
