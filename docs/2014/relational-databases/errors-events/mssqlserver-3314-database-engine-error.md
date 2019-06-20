---
title: MSSQLSERVER_3314 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3314 (Database Engine error)
ms.assetid: f3a5ca6a-b502-4cab-b3b1-4bc753763fa9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b8d82911f013c9284a55bd55f00654a98633df0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914164"
---
# <a name="mssqlserver3314"></a>MSSQLSERVER_3314
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3314|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|ERR_LOG_RID2|  
|消息正文|在数据库 '%.*ls' 中撤消日志记录下的操作时，在日志记录 %S_LSN 处出错。 通常，这一特定故障以前在 Windows 事件日志服务中会记录为错误。 请利用备份还原数据库或文件，或者修复该数据库。|  
  
## <a name="explanation"></a>解释  
 这是撤消恢复的累积错误。 此错误使数据库进入 SUSPECT 状态。 主文件组以及可能其他文件组可疑并可能受损。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动过程中无法恢复数据库，因此无法使用该数据库。 需要用户执行操作来解决问题。  
  
 请注意，如果对于 **tempdb**发生此错误，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例关闭。  
  
## <a name="user-action"></a>用户操作  
 此错误可能是由在某次尝试启动服务器实例或恢复数据库的过程中系统上存在的暂时性条件导致的。 此错误也可能是由当您每次尝试启动数据库时发生的永久性错误导致的。 有关原因的信息，请检查 Windows 事件日志以了解有关指示特定故障的先前错误。  
  
 有关错误 3314 出现原因的信息，请检查 Windows 事件日志以了解有关指示特定故障的先前错误。 相应的用户操作取决于 Windows 事件日志中的信息是否指示该 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误由暂时条件或永久性故障导致。 有关排除 3314 错误的用户操作的信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书。  
  
## <a name="see-also"></a>请参阅  
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)   
 [DBCC CHECKDB (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [完整数据库还原（简单恢复模式）](../backup-restore/complete-database-restores-simple-recovery-model.md)   
 [MSSQLSERVER_824](mssqlserver-824-database-engine-error.md)   
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
