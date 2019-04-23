---
title: 到 SMO 的 SQL-DMO 映射 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 590f5396-98d5-485e-9b41-728c6ed7cb9d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a6273032f88807291bfc7024f1abcdbd1440073
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158413"
---
# <a name="sql-dmo-mapping-to-smo"></a>SQL-DMO 到 SMO 的映射
  SQL 分布式管理对象 (SQL-DMO) 不再包含在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，应转换 SQL-DMO 应用程序以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象 (SMO)。 SMO 对象模型类似于 SQL-DMO，所以多数 SQL-DMO 对象映射到 SMO 中同名的对象。 但是，在转换到 SMO 的过程中，更改或删除了一些 SQL-DMO 对象。 下表列出建议对未直接转换为 SMO 的 SQL-DMO 对象采取的操作。  
  
|SQL-DMO 对象|SMO 中的操作|  
|---------------------|-------------------|  
|View2 对象|已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空间。|  
|AlertSystem 对象|已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空间。|  
|Application 对象|已删除。|  
|Backup 对象和 Backup2 对象|<xref:Microsoft.SqlServer.Management.Smo.Backup> 和 <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase> 对象。|  
|BackupDevice 对象|<xref:Microsoft.SqlServer.Management.Smo.BackupDevice> 对象|  
|BulkCopy 对象和 BulkCopy2 对象|已删除并由 <xref:Microsoft.SqlServer.Management.Smo.Transfer> 对象代替。|  
|Category 对象|已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空间。 已由 <xref:Microsoft.SqlServer.Management.Smo.Agent.AlertCategory>、<xref:Microsoft.SqlServer.Management.Smo.Agent.OperatorCategory> 和 <xref:Microsoft.SqlServer.Management.Smo.Agent.JobCategory> 对象代替。|  
|Check 对象|（属于<xref:Microsoft.SqlServer.Management.Smo.Check> 对象）的父级。|  
|Column 对象和 Column2 对象|<xref:Microsoft.SqlServer.Management.Smo.Column> 对象。|  
|Configuration 对象|<xref:Microsoft.SqlServer.Management.Smo.Configuration> 和 <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase> 对象。|  
|ConfigValue 对象|<xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> 对象。|  
|Database 对象和 Database2 对象|<xref:Microsoft.SqlServer.Management.Smo.Database> 对象。|  
|DatabaseRole 对象和 DatabaseRole2 对象|<xref:Microsoft.SqlServer.Management.Smo.DatabaseRole> 对象。|  
|DBFile 对象|<xref:Microsoft.SqlServer.Management.Smo.DataFile> 对象。|  
|DBOption 对象和 DBOption2 对象|已移入 <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions> 对象中。|  
|Default 对象和 Default2 对象|<xref:Microsoft.SqlServer.Management.Smo.Default> 对象。|  
|DistributionArticle 对象和 DistributionArticle2 对象|移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|DistributionDatabase 对象和 DistributionDatabase2 对象|移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|DistributionPublication 对象和 DistributionPublication2 对象|移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|DistributionSubscription 对象和 DistributionSubscription2 对象|移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|Distributor 对象和 Distributor2 对象|移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|DRIDefault 对象|已移至 <xref:Microsoft.SqlServer.Management.Smo.ScriptingOptions> 对象。|  
|FileGroup 对象和 FileGroup2 对象|<xref:Microsoft.SqlServer.Management.Smo.FileGroup> 对象。|  
|FullTextCatalog 对象和 FullTextCatalog2 对象|<xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> 和 <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex> 对象。|  
|Index 对象和 Index2 对象|（属于<xref:Microsoft.SqlServer.Management.Smo.Index> 对象）的父级。|  
|IntegratedSecurity 对象|功能已移至 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 命名空间中的 <xref:Microsoft.SqlServer.Management.Common> 对象。|  
|Job 对象|<xref:Microsoft.SqlServer.Management.Smo.Agent.Job> 对象。 移动到<xref:Microsoft.SqlServer.Management.Smo.Agent>命名空间。|  
|JobFilter 对象|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobFilter> 对象。 移动到<xref:Microsoft.SqlServer.Management.Smo.Agent>命名空间。|  
|JobHistoryFilter 对象|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobHistoryFilter> 对象。 移动到<xref:Microsoft.SqlServer.Management.Smo.Agent>命名空间。|  
|JobSchedule 对象|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobSchedule> 对象。 移动到<xref:Microsoft.SqlServer.Management.Smo.Agent>命名空间。|  
|JobServer 对象和 JobServer2 对象|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobServer> 对象。 移动到<xref:Microsoft.SqlServer.Management.Smo.Agent>命名空间。|  
|JobStep 对象|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobStep> 对象。 移动到<xref:Microsoft.SqlServer.Management.Smo.Agent>命名空间。|  
|Key 对象|<xref:Microsoft.SqlServer.Management.Smo.ForeignKey> 和 <xref:Microsoft.SqlServer.Management.Smo.Index> 对象。|  
|LinkedServer 对象和 LinkedServer2 对象|<xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 对象。|  
|LinkedServerLogin 对象|<xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> 对象。|  
|LogFile 对象|<xref:Microsoft.SqlServer.Management.Smo.LogFile> 对象。|  
|Login 对象和 Login2 对象|<xref:Microsoft.SqlServer.Management.Smo.Login> 对象。|  
|MergeArticle 对象和 MergeArticle2 对象|<xref:Microsoft.SqlServer.Replication.MergeArticle> 对象。 移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|MergeDynamicSnapshotJob 对象|移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|MergePublication 对象和 MergePublication2 对象|<xref:Microsoft.SqlServer.Replication.MergePublication> 对象。 移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|MergePullSubscription 对象和 MergePullSubscription2 对象|<xref:Microsoft.SqlServer.Replication.MergePullSubscription> 对象。 移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|MergeSubscription 对象|<xref:Microsoft.SqlServer.Replication.MergeSubscription> 对象。 移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|MergeSubsetFilter 对象|移动到`N:Microsoft.SqlServer.Replication`命名空间。|  
|NameList 对象|已删除。 <xref:Microsoft.SqlServer.Management.Smo.Scripter> 对象中的替代功能。|  
|Operator 对象|移动到<xref:Microsoft.SqlServer.Management.Smo.Agent>命名空间。|  
|Permission 对象和 Permission2 对象|<xref:Microsoft.SqlServer.Management.Smo.ServerPermission>、<xref:Microsoft.SqlServer.Management.Smo.DatabasePermission>、<xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> 和 <xref:Microsoft.SqlServer.Management.Smo.ObjectPermission> 对象。|  
|Property 对象|`Property` 对象。|  
|Publisher 对象和 Publisher2 对象|<xref:Microsoft.SqlServer.Replication.ReplicationServer> 对象。 移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|QueryResults 对象和 QueryResults2 对象|已由 <xref:System.Data.DataTable> 或 <xref:System.Data.DataSet> 系统对象代替。|  
|RegisteredServer 对象|移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|RegisteredSubscriber 对象|移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|Registry 对象和 Registry2 对象|已删除。|  
|RemoteLogin 对象|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> 对象。 已移至公共命名空间。|  
|RemoteServer 对象和 RemoteServer2 对象|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> 对象。 移动到<xref:Microsoft.SqlServer.Management.Common>命名空间。|  
|Replication 对象|移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|ReplicationDatabase 对象和 ReplicationDatabase2 对象|<xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 对象。 移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|ReplicationSecurity 对象|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> 对象。 移动到<xref:Microsoft.SqlServer.Management.Common>命名空间。|  
|ReplicationStoredProcedure 对象和 ReplicationStoredProcedure2 对象|<xref:Microsoft.SqlServer.Replication.ReplicationStoredProcedure> 对象。 移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|ReplicationTable 对象和 ReplicationTable2 对象|<xref:Microsoft.SqlServer.Replication.ReplicationTable> 对象。 移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|Restore 对象和 Restore2 对象|<xref:Microsoft.SqlServer.Management.Smo.Restore> 和 <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase> 对象。|  
|Rule 对象和 Rule2 对象|（属于<xref:Microsoft.SqlServer.Management.Smo.Rule> 对象）的父级。|  
|Schedule 对象|移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|ServerGroup 对象|已删除。|  
|ServerRole 对象|<xref:Microsoft.SqlServer.Management.Smo.ServerRole> 对象。|  
|SQLObjectList 对象|<xref:Microsoft.SqlServer.Management.Smo.SqlSmoObject> 数组。|  
|SQLServer 对象和 SQLServer2 对象|<xref:Microsoft.SqlServer.Management.Smo.Server> 对象。|  
|StoredProcedure 对象和 StoredProcedure2 对象|<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> 和 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> 对象|  
|Subscriber 对象和 Subscriber2 对象|移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|SystemDatatype 对象和 SystemDataType2 对象|<xref:Microsoft.SqlServer.Management.Smo.DataType> 对象。|  
|Table 对象和 Table2 对象|<xref:Microsoft.SqlServer.Management.Smo.Table> 对象。|  
|TargetServer 对象|移动到<xref:Microsoft.SqlServer.Management.Smo.Agent>命名空间。|  
|TargetServerGroup 对象|移动到<xref:Microsoft.SqlServer.Management.Smo.Agent>命名空间。|  
|TransactionLog 对象|功能已移入 <xref:Microsoft.SqlServer.Management.Smo.Database> 对象中。|  
|TransArticle 对象和 TransArticle2 对象|<xref:Microsoft.SqlServer.Replication.TransArticle> 对象。 移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|Transfer 对象和 Transfer2 对象|<xref:Microsoft.SqlServer.Management.Smo.Transfer> 对象。|  
|TransPublication 对象和 TransPublication2 对象|<xref:Microsoft.SqlServer.Replication.TransPublication> 对象。 移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|TransPullSubscription 对象和 TransPullSubscription2 对象|<xref:Microsoft.SqlServer.Replication.TransPullSubscription> 对象。 移动到<xref:Microsoft.SqlServer.Replication>命名空间。|  
|Trigger 对象和 Trigger2 对象|<xref:Microsoft.SqlServer.Management.Smo.Trigger> 对象。|  
|User 对象和 User2 对象|<xref:Microsoft.SqlServer.Management.Smo.User> 对象。|  
|UserDefinedDatatype 对象和 UserDefinedDataType2 对象|<xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> 对象。|  
|UserDefinedFunction 对象|<xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> 和 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter> 对象。|  
|View 对象和 View2 对象|<xref:Microsoft.SqlServer.Management.Smo.View> 对象。|  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 管理对象 (SMO) 编程指南](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
