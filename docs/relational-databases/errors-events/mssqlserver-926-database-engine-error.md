---
description: MSSQLSERVER_926
title: MSSQLSERVER_926 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 926 (Database Engine error)
ms.assetid: 57e01668-883b-4be4-84a8-a111caaf0486
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 854648c2971c1cc7f49f52c0a45b761367c64f25
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88330933"
---
# <a name="mssqlserver_926"></a>MSSQLSERVER_926
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|926|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DB_SUSPECT|  
|消息正文|无法打开数据库 '%.*ls'。 恢复操作已将该数据库标记为 SUSPECT。 有关详细信息，请参阅 SQL Server 错误日志。|  
  
## <a name="explanation"></a>说明  
由于将数据库变为一致事务状态的恢复进程失败，因此该数据库被标记为可疑。 这可能出现在下列操作过程中：  
  
-   启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  
  
-   附加数据库。  
  
-   使用 RESTORE 数据库或 RESTORE LOG 过程。  
  
## <a name="user-action"></a>用户操作  
检查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志并确定错误原因。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自恢复失败后已重新启动，请参见先前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志以查看恢复失败的原因。  
  
如果恢复是由于持久性 I/O 错误、页撕裂或其他可能的硬件问题而失败，请解决底层硬件的问题并使用备份还原数据库。 如果没有可用的备份，请考虑 DBCC CHECKDB 的修复选项。  
  
如果您无法解决此问题，请与主要支持提供商联系。 保存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志以便进行查看。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server 数据库的备份和还原](~/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
[sys.sysdatabases (Transact-SQL)](~/relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)  
[数据库分离和附加 (SQL Server)](~/relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
