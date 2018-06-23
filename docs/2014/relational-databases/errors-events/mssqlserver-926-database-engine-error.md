---
title: MSSQLSERVER_926 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 926 (Database Engine error)
ms.assetid: 57e01668-883b-4be4-84a8-a111caaf0486
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5078b002ef19d548bed73dac73cc8d960d967d99
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125856"
---
# <a name="mssqlserver926"></a>MSSQLSERVER_926
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|926|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DB_SUSPECT|  
|消息正文|无法打开数据库 '%.*ls'。 恢复操作已将该数据库标记为 SUSPECT。 有关详细信息，请参阅 SQL Server 错误日志。|  
  
## <a name="explanation"></a>解释  
 由于将数据库变为一致事务状态的恢复进程失败，因此该数据库被标记为可疑。 这可能出现在下列操作过程中：  
  
-   启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  
  
-   附加数据库。  
  
-   使用 RESTORE 数据库或 RESTORE LOG 过程。  
  
## <a name="user-action"></a>用户操作  
 检查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志并确定错误原因。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自恢复失败后已重新启动，请参见先前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志以查看恢复失败的原因。  
  
 如果恢复是由于持久性 I/O 错误、页撕裂或其他可能的硬件问题而失败，请解决底层硬件的问题并使用备份还原数据库。 如果没有可用的备份，请考虑 DBCC CHECKDB 的修复选项。  
  
 如果您无法解决此问题，请与主要支持提供商联系。 保存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志以便进行查看。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 数据库的备份和还原](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [sys.sysdatabases &#40;Transact SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql)   
 [数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
