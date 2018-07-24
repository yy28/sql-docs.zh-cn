---
title: sqllogship 应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: sqllogship
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sqllogship
ms.assetid: 8ae70041-f3d9-46e4-8fa8-31088572a9f8
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1ce23bc4217f4bc538de0ddc1dbbaf8284a3c177
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37969083"
---
# <a name="sqllogship-application"></a>sqllogship 应用程序
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **sqllogship** 应用程序用于执行日志传送配置中的备份、复制或还原操作以及相关的清理任务。 这些操作是在特定的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上针对特定数据库执行的。  
  
 ![主题链接图标](../database-engine/configure-windows/media/topic-link.gif "主题链接图标")语法约定，请参阅[命令提示实用工具参考&#40;数据库引擎&#41;](../tools/command-prompt-utility-reference-database-engine.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqllogship -server instance_name { -backup primary_id | -copy secondary_id | -restore secondary_id } [ –verboselevel level ] [ –logintimeout timeout_value ] [ -querytimeout timeout_value ]  
```  
  
## <a name="arguments"></a>参数  
 **-server** *instance_name*  
 指定将在其上运行操作的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例。 要指定的服务器实例取决于所指定的日志传送操作。 对于 **-backup**， *instance_name* 必须为日志传送配置中主服务器的名称。 对于 **-copy** 或 **-restore**， *instance_name* 必须为日志传送配置中辅助服务器的名称。  
  
 **-backup** *primary_id*  
 执行主数据库的备份操作，此数据库的主 ID 由 *primary_id*指定。 可以通过从 [log_shipping_primary_databases](../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md) 系统表选择此 ID 或通过使用 [sp_help_log_shipping_primary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md) 存储过程来获取此 ID。  
  
 备份操作将在备份目录中创建日志备份。 然后， **sqllogship** 应用程序会根据文件保持期清除任何旧备份文件。 接着，此应用程序记录在主服务器和监视服务器上执行备份操作的历史记录。 最后，此应用程序会运行 [sp_cleanup_log_shipping_history](../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)，根据保持期清除旧的历史记录信息。  
  
 **-copy** *secondary_id*  
 执行复制操作，以便复制指定辅助服务器上一个或多个辅助数据库的备份，辅助数据库的辅助 ID 由 *secondary_id*指定。 可以通过从 [log_shipping_secondary](../relational-databases/system-tables/log-shipping-secondary-transact-sql.md) 系统表选择此 ID 或通过使用 [sp_help_log_shipping_secondary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md) 存储过程来获取此 ID。  
  
 此操作将备份文件从备份目录复制到目标目录。 然后， **sqllogship** 应用程序会记录在辅助服务器和监视服务器上执行复制操作的历史记录。  
  
 **-restore** *secondary_id*  
 在指定辅助服务器上对一个或多个辅助数据库执行还原操作，辅助数据库的辅助 ID 由 *secondary_id*指定。 可以通过使用 **sp_help_log_shipping_secondary_database** 存储过程获取此 ID。  
  
 目标目录中在最近还原点之后创建的所有备份文件都将还原到一个或多个辅助数据库中。 然后， **sqllogship** 应用程序会根据文件保持期清除任何旧备份文件。 接着，此应用程序记录在辅助服务器和监视服务器上执行还原操作的历史记录。 最后，此应用程序会运行 **sp_cleanup_log_shipping_history**，根据保持期清除旧的历史记录信息。  
  
 **–verboselevel** *level*  
 指定要添加到日志传送历史记录的消息的级别。 *level* 是以下整数之一：  
  
|level|描述|  
|-----------|-----------------|  
|0|不输出跟踪消息和调试消息。|  
|@shouldalert|输出错误处理消息。|  
|2|输出警告消息和错误处理消息。|  
|**3**|输出信息性消息、警告和错误处理消息。 这是默认值。|  
|4|输出所有调试消息和跟踪消息。|  
  
 **–logintimeout** *timeout_value*  
 指定所分配的在登录尝试超时之前可用于尝试登录到服务器实例的时间。默认值为 15 秒。 timeout_value 为 int。  
  
 **-querytimeout** *timeout_value*  
 指定所分配的在尝试启动指定操作超时之前的尝试时间。默认情况下不指定超时期限。 timeout_value 为 int。  
  
## <a name="remarks"></a>Remarks  
 我们建议您尽可能使用备份、复制和还原作业来执行备份、复制和还原操作。 若要从批处理操作或其他应用程序启动这些作业，请调用 [sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md) 存储过程。  
  
 由 **sqllogship** 创建的日志传送历史记录与由日志传送备份、复制和还原作业创建的历史记录混杂在一起。 如果打算反复使用 **sqllogship** 来执行日志传送配置中的备份、复制或还原操作，请考虑禁用相应的日志传送作业。 有关详细信息，请参阅 [Disable or Enable a Job](http://msdn.microsoft.com/library/5041261f-0c32-4d4a-8bee-59a6c16200dd)。  
  
 **sqllogship** 应用程序 SqlLogShip.exe 安装在 x:\Program Files\Microsoft SQL Server\130\Tools\Binn 目录中。  
  
## <a name="permissions"></a>Permissions  
 **sqllogship** 使用 Windows 身份验证。 运行此命令所使用的 Windows 身份验证帐户需要 Windows 目录访问权限和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 权限。 要求取决于 **sqllogship** 命令是指定 **-backup**、 **-copy**还是 **-restore** 选项。  
  
|选项|目录访问权限|Permissions|  
|------------|----------------------|-----------------|  
|**-backup**|需要对备份目录的读/写访问权限。|需要与 BACKUP 语句相同的权限。 有关详细信息，请参阅 [BACKUP (Transact-SQL)](../t-sql/statements/backup-transact-sql.md)。|  
|**-copy**|需要对备份目录的读取访问权限以及对复制目录的写入访问权限。|需要与 [sp_help_log_shipping_secondary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md) 存储过程相同的权限。|  
|**-restore**|需要对复制目录的读/写访问权限。|需要与 RESTORE 语句相同的权限。 有关详细信息，请参阅 [RESTORE (Transact-SQL)](../t-sql/statements/restore-statements-transact-sql.md)。|  
  
> [!NOTE]  
>  若要找出备份和复制目录的路径，可以运行 **sp_help_log_shipping_secondary_database** 存储过程或查看 **msdb** 中的 **log_shipping_secondary** 表。 备份目录和目标目录的路径分别位于 **backup_source_directory** 和 **backup_destination_directory** 列。  
  
## <a name="see-also"></a>另请参阅  
 [关于日志传送 (SQL Server)](../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_primary_databases (Transact-SQL)](../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)   
 [log_shipping_secondary (Transact-SQL)](../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)   
 [sp_cleanup_log_shipping_history (Transact-SQL)](../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_help_log_shipping_primary_database (Transact-SQL)](../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database (Transact-SQL)](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [sp_start_job (Transact-SQL)](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)  
  
  
