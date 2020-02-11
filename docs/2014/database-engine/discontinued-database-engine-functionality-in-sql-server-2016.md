---
title: SQL Server 2014 中的废止数据库引擎功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- VIA protocol
- unsupported features [SQL Server]
- SQL Mail
- discontinued functionality [SQL Server]
- RESTORE WITH DBO_ONLY
- BACKUP WITH PASSWORD
- user instances enabled
- BACKUP WITH MEDIAPASSWORD
- AWE
- SQL-DMO
- '*= and =*'
- 80 compatibility levels
- COMPUTE BY
- user instance timeout
- sp_dropalias
- COMPUTE
- WITH APPEND
- sys.database_principal_aliases
- sp_dboption
- DATABASEPROPERTY
- FASTFIRSTROW hint
- SET DISABLE_DEF_CNST_CHK
ms.assetid: d686cdf0-d11d-4dba-9ec8-de1a5f189f25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2ebb9b4e3db7cf8f7a19fd582dceb0b19f5c47d0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67463467"
---
# <a name="discontinued-database-engine-functionality-in-sql-server-2014"></a>SQL Server 2014 中废止的数据库引擎功能
  本主题介绍 [!INCLUDE[ssDE](../includes/ssde-md.md)] 中不再可用的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。  
  
## <a name="SQL14"></a>中废止的功能[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 下表列出了 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]中移除的功能。  
  
|类别|已不再使用的功能|替代功能|  
|--------------|--------------------------|-----------------|  
|兼容级别|90 兼容性级别|必须将数据库的兼容性级别至少设置为 100。 当兼容性级别低于 100 的数据库升级到 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]时，在升级操作过程中数据库的兼容性级别将设置为 100。|  
  
## <a name="Denali"></a>中废止的功能[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 下表列出了 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]中移除的功能。  
  
|类别|已不再使用的功能|替代功能|  
|--------------|--------------------------|-----------------|  
|备份和还原|已停止使用 PASSWORD 和**backup {database &#124; log}** 的**backup {database &#124; log}** MEDIAPASSWORD。 **RESTORE {DATABASE &#124; LOG} WITH [MEDIA] PASSWORD**仍不推荐使用。|无|  
|备份和还原|**还原 {数据库 &#124; 日志} .。。与 DBO_ONLY**|**还原 {DATABASE &#124; LOG} ... .。。与 RESTRICTED_USER**|  
|兼容级别|80 兼容级别|必须将数据库的兼容级别至少设置为 90。|  
|配置选项|`sp_configure 'user instance timeout'` 和 `'user instances enabled'`|使用本地数据库功能。 有关详细信息，请参阅[SqlLocalDB 实用工具](../tools/sqllocaldb-utility.md)|  
|连接协议|不再支持 VIA 协议。|请改用 TCP。|  
|数据库对象|有关触发器的 `WITH APPEND` 子句|重新创建整个触发器。|  
|数据库选项|`sp_dboption`|`ALTER DATABASE`|  
|Mail|SQL Mail|使用数据库邮件。 有关详细信息，请参阅 [Database Mail](../relational-databases/database-mail/database-mail.md) 和  [Use Database Mail Instead of SQL Mail](../relational-databases/policy-based-management/use-database-mail-instead-of-sql-mail.md)。|  
|内存管理|32 位地址窗口化扩展插件 (AWE) 和 32 位热添加内存支持。|使用 64 位操作系统。|  
|元数据|`DATABASEPROPERTY`|`DATABASEPROPERTYEX`|  
|可编程性|SQL Server 分布式管理对象 (SQL-DMO)|SQL Server 管理对象 (SMO)|  
|查询提示|`FASTFIRSTROW`提示|`OPTION (FAST`*n* `)`。|  
|远程服务器|用户通过 `sp_addserver` 创建新的远程服务器的功能已停止使用。 带有“local”选项的 `sp_addserver` 保持可用。 可以使用在升级过程中保留或由复制创建的远程服务器。|用链接服务器替代远程服务器。|  
|安全性|`sp_dropalias`|请将别名替换为用户帐户和数据库角色的组合。 请使用 `sp_dropalias` 删除已升级数据库中的别名。|  
|安全性|表示来自早于 **2000 的登录值的** PWDCOMPARE [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的版本参数不再使用。|无|  
|SMO 中的 Service Broker 可编程性|
  **Microsoft.SqlServer.Management.Smo.Broker.BrokerPriority** 类不再实现 **Microsoft.SqlServer.Management.Smo.IObjectPermission** 接口。||  
|SET 选项|`SET DISABLE_DEF_CNST_CHK`|无。|  
|系统表|sys.database_principal_aliases|请使用角色而不是别名。|  
|Transact-SQL|格式为 `RAISERROR` 的 `RAISERROR integer 'string'` 不再使用。|使用当前的**RAISERROR （...）** 语法重写语句。|  
|Transact-SQL 语法|`COMPUTE / COMPUTE BY`|使用 `ROLLUP`|  
|Transact-SQL 语法|使用 and **=&#42;** ** \* **|使用 ANSI 联接语法。 有关详细信息，请参阅 [FROM (Transact-SQL).](https://msdn.microsoft.com/library/ms177634\(SQL.105\).aspx)|  
|XEvents|databases_data_file_size_changed、databases_log_file_size_changed<br /><br /> eventdatabases_log_file_used_size_changed<br /><br /> locks_lock_timeouts_greater_than_0<br /><br /> locks_lock_timeouts|替换为 database_file_size_change event、database_file_size_change<br /><br /> database_file_size_change event<br /><br /> lock_timeout_greater_than_0<br /><br /> lock_timeout|  
  
 **其他 XEvent 更改**  
  
 **resource_monitor_ring_buffer_record**：  
  
-   删除的字段：single_pages_kb、multiple_pages_kb  
  
-   添加的字段：target_kb、pages_kb  
  
 **memory_node_oom_ring_buffer_recorded**：  
  
-   删除的字段：single_pages_kb、multiple_pages_kb  
  
-   添加的字段：target_kb、pages_kb  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2014 中不推荐使用的数据库引擎功能](deprecated-database-engine-features-in-sql-server-2016.md?view=sql-server-2014)  
  
  
