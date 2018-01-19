---
title: SHUTDOWN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHUTDOWN_TSQL
- SHUTDOWN
dev_langs: TSQL
helpviewer_keywords:
- SQL Server, stopping
- shutting down SQL Server
- SHUTDOWN statement
- stopping SQL Server
- immediately stopping SQL Server
ms.assetid: c8b03ff9-688c-4fe8-86e8-bd6bd401c9a4
caps.latest.revision: "31"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e4cf8ea2b61d4f1acb69ea489a5116a701264469
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="shutdown-transact-sql"></a>SHUTDOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  立即停止 SQL Server。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SHUTDOWN [ WITH NOWAIT ]   
```  
  
## <a name="arguments"></a>参数  
 WITH NOWAIT  
 選擇性。 在不对每个数据库执行检查点操作的情况下关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在尝试终止全部用户进程后退出。 服务器重新启动时，将针对未完成事务执行回滚操作。  
  
## <a name="remarks"></a>注释  
 除非使用 WITHNOWAIT 选项，则关闭关闭[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过：  
  
1.  禁用登录名 (除外的成员**sysadmin**和**serveradmin**固定服务器角色的成员)。  
  
    > [!NOTE]  
    >  若要显示所有当前用户的列表，请运行**sp_who**。  
  
2.  等待当前正在运行的 Transact-SQL 语句或存储过程完成。 若要显示的所有活动进程和锁列表，请运行**sp_who**和**sp_lock**分别。  
  
3.  在每个数据库中插入检查点。  
  
 使用关闭语句最大程度减少量的自动恢复工作时需要的成员**sysadmin**固定服务器角色重新启动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 还可以使用其他工具和方法停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 每个工具或方法都在所有数据库内执行检查点。 您可以从数据缓存中刷新已提交的数据，然后停止服务器：  
  
-   通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器。  
  
-   通过运行**net 停止 mssqlserver**在命令提示符下，对于默认实例，或通过运行 **net stop mssql$ * * * instancename*从命令提示符对于命名实例。  
  
-   使用“控制面板”中的“服务”应用程序。  
  
 如果**sqlservr.exe**启动命令提示符下，按 CTRL + C 关闭[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 然而，按 Ctrl+C 键将不插入检查点。  
  
> [!NOTE]  
>  使用上述任何方法停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都会向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发送 `SERVICE_CONTROL_STOP` 消息。  
  
## <a name="permissions"></a>权限  
 关闭权限分配给的成员**sysadmin**和**serveradmin**固定的服务器角色，并且它们不可转让。  
  
## <a name="see-also"></a>另请参阅  
 [检查点 &#40;Transact SQL &#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sqlservr 应用程序](../../tools/sqlservr-application.md)   
 [启动、停止、暂停、继续、重新启动数据库引擎、SQL Server 代理或 SQL Server Browser 服务](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
