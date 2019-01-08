---
title: 启用和禁用变更数据捕获 (SQL Server) | Microsoft Docs
ms.date: 01/02/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data capture [SQL Server], enabling tables
- change data capture [SQL Server], enabling databases
- change data capture [SQL Server], disabling databases
- change data capture [SQL Server], disabling tables
ms.assetid: b741894f-d267-4b10-adfe-cbc14aa6caeb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 61ca34394e2cab5cf16862f6ddae20573c4e17a0
ms.sourcegitcommit: a11e733bd417905150567dfebc46a137df85a2fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991830"
---
# <a name="enable-and-disable-change-data-capture-sql-server"></a>启用和禁用变更数据捕获 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
  本主题说明如何对数据库和表启用和禁用变更数据捕获。  
  
## <a name="enable-change-data-capture-for-a-database"></a>对数据库启用变更数据捕获  
 在为各个表创建捕获实例之前，必须先由 **sysadmin** 固定服务器角色的成员对数据库启用变更数据捕获。 通过在数据库上下文中运行 [sys.sp_cdc_enable_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md) 存储过程可实现这一点。 若要确定数据库是否已启用此项功能，请在 **sys.databases** 目录视图中查询 **is_cdc_enabled** 列。  
  
 当对数据库启用了变更数据捕获之后，将为数据库创建 **cdc** 架构、 **cdc** 用户、元数据表和其他系统对象。 **cdc** 架构包含变更数据捕获元数据表，当对源表启用了变更数据捕获之后，各个更改表将用作更改数据的存储库。 **cdc** 架构还包含用于查询更改数据的关联系统函数。  
  
 变更数据捕获要求采用独占方式使用 **cdc** 架构和 **cdc** 用户。 如果某数据库中当前存在名为 *cdc* 的架构或数据库用户，那么在删除或重命名此架构或用户之前，不能对此数据库启用变更数据捕获。  
  
 有关启用数据库的示例，请参阅 Enable Database for Change Data Capture 模板。  
  
> [!IMPORTANT]  
>  若要在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中找到模板，请转至 **“视图”**，单击 **“模板资源管理器”**，然后选择 **“SQL Server 模板”**。 **Change Data Capture** 为一个子文件夹。 在此文件夹下，您会找到本主题中提到的所有模板。 **工具栏上还有一个** “模板资源管理器” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 图标。  
  
```sql  
-- ====  
-- Enable Database for CDC template   
-- ====  
USE MyDB  
GO  
EXEC sys.sp_cdc_enable_db  
GO  
```  
  
## <a name="disable-change-data-capture-for-a-database"></a>对数据库禁用变更数据捕获  
 **sysadmin** 固定服务器角色的成员可以在数据库上下文中运行存储过程 [sys.sp_cdc_disable_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) 以对数据库禁用变更数据捕获。 在禁用数据库之前不必禁用各个表。 禁用数据库会删除所有关联的变更数据捕获元数据，包括 **cdc** 用户、架构和变更数据捕获作业。 但是，任何由变更数据捕获创建的访问控制角色不会被自动删除，而是必须将其显式删除。 若要确定数据库是否已启用此项功能，请在 sys.databases 目录视图中查询 **is_cdc_enabled** 列。  
  
 当删除启用了变更数据捕获的数据库时会自动删除变更数据捕获作业。  
  
 有关禁用数据库的示例，请参阅 Disable Database for Change Data Capture 模板。  
  
> [!IMPORTANT]  
>  若要在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中找到模板，请转至 **“视图”**，单击 **“模板资源管理器”**，然后单击 **“SQL Server 模板”**。 **“变更数据捕获”** 为子文件夹，在该文件夹中您将找到本主题中提到的所有模板。 **工具栏上还有一个** “模板资源管理器” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 图标。  
  
```sql  
-- =======  
-- Disable Database for Change Data Capture template   
-- =======  
USE MyDB  
GO  
EXEC sys.sp_cdc_disable_db  
GO  
```  
  
## <a name="enable-change-data-capture-for-a-table"></a>对表启用变更数据捕获  
 在对数据库启用变更数据捕获之后， **db_owner** 固定数据库角色的成员即可以使用存储过程 **sys.sp_cdc_enable_table**为各个源表创建捕获实例。 若要确定是否已对某个源表启用了变更数据捕获，请在 **sys.tables** 目录视图中检查 is_tracked_by_cdc 列。  
  
 创建捕获实例时，可以指定以下选项：  
  
 **Columns in the source table to be captured**。  
  
 默认情况下，源表中的所有列都将标识为已捕获列。 如果只需要跟踪这些列中的部分列（如出于隐私或性能方面的原因），请使用 *@captured_column_list* 参数指定这些列的子集。  
  
 **包含更改表的文件组。**  
  
 默认情况下，更改表位于数据库的默认文件组中。 希望控制各个更改表放置位置的数据库所有者可以使用 *@filegroup_name* 参数为与该捕获实例相关的更改表指定一个特定的文件组。 指定的文件组必须已存在。 通常建议将更改表置于独立于源表的文件组中。 有关演示 *@filegroup_name* 参数使用方法的示例，请参阅**通过指定文件组选项启用表**模板。  
  
```sql  
-- =========  
-- Enable a Table Specifying Filegroup Option Template  
-- =========  
USE MyDB  
GO  
  
EXEC sys.sp_cdc_enable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@role_name     = N'MyRole',  
@filegroup_name = N'MyDB_CT',  
@supports_net_changes = 1  
GO  
```  
  
 **控制对更改表的访问的角色。**  
  
 指定角色的目的是控制对更改数据的访问。 指定的角色可以为现有的固定服务器角色或数据库角色。 如果指定的角色还不存在，则会自动创建具有该名称的数据库角色。 **sysadmin** 或 **db_owner** 角色的成员对更改表中的数据拥有完全访问权限。 所有其他用户必须对源表中的所有捕获列拥有 SELECT 权限。 此外，当指定角色时，不是 **sysadmin** 或 **db_owner** 角色成员的用户还必须是指定角色的成员。  
  
 如果不想使用访问控制角色，请将 *@role_name* 参数显式设置为 NULL。 有关如何在没有访问控制角色的情况下启用表的示例，请参阅 **Enable a Table Without Using a Gating Role** 模板。  
  
```sql  
-- =========  
-- Enable a Table Without Using a Gating Role template   
-- =========  
USE MyDB  
GO  
EXEC sys.sp_cdc_enable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@role_name     = NULL,  
@supports_net_changes = 1  
GO  
  
```  
  
 **查询净更改的函数。**  
  
 捕获实例将始终包含一个表值函数以返回在指定的时间间隔内出现的所有更改表项。 此函数通过在“cdc.fn_cdc_get_all_changes_”后追加捕获实例名称来命名。 有关详细信息，请参阅 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  (Transact-SQL)](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)。  
  
 如果将参数 *@supports_net_changes* 设为 1，还将为捕获实例生成一个净更改函数。 对于在调用中指定的时间间隔内发生更改的每个非重复行，此函数仅返回一项更改。 有关详细信息，请参阅[cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; (Transact-SQL)](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)。  
  
 若要支持净更改查询，源表必须具有用于唯一标识行的主键或唯一索引。 如果使用了唯一索引，则必须使用 *@index_name* 参数指定索引名称。 在主键或唯一索引中定义的列必须包含在要捕获的源列列表中。  
  
 有关演示如何创建同时具有这两个查询函数的捕获实例的示例，请参阅 **Enable a Table for All and Net Changes Queries** 模板。  
  
```sql  
-- =============  
-- Enable a Table for All and Net Changes Queries template   
-- =============  
USE MyDB  
GO  
EXEC sys.sp_cdc_enable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@role_name     = N'MyRole',  
@supports_net_changes = 1  
GO  
```  
  
> [!NOTE]
>  如果对具有现有主键的表启用变更数据捕获，且未使用 *@index_name* 参数来标识备用的唯一索引，则变更数据捕获功能将使用主键。 只有先对表禁用变更数据捕获，才能对主键进行后续更改。 无论配置变更数据捕获时是否要求支持净更改查询均是如此。 如果对表启用变更数据捕获时该表中没有主键，则变更数据捕获将忽略后来添加的主键。 由于变更数据捕获不会使用在启用表之后创建的主键，因此可以不受限制地将该键及键列删除。  
  
## <a name="disable-change-data-capture-for-a-table"></a>对表禁用变更数据捕获  
 **db_owner** 固定数据库角色的成员可以通过使用存储过程 **sys.sp_cdc_disable_table**为各个源表删除捕获实例。 若要确定是否已对某个源表当前启用了变更数据捕获，请在 **sys.tables** 目录视图中检查 **is_tracked_by_cdc** 列。 如果在禁用发生后没有对数据库启用任何表，则还会删除变更数据捕获作业。  
  
 如果删除了启用变更数据捕获的表，则会自动删除与该表关联的变更数据捕获元数据。  
  
 有关禁用表的示例，请参阅 Disable a Capture Instance for a Table 模板。  
  
```sql  
-- =====  
-- Disable a Capture Instance for a Table template   
-- =====  
USE MyDB  
GO  
EXEC sys.sp_cdc_disable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@capture_instance = N'dbo_MyTable'  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [跟踪数据更改 (SQL Server)](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [关于变更数据捕获 (SQL Server)](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [处理变更数据 (SQL Server)](../../relational-databases/track-changes/work-with-change-data-sql-server.md)   
 [管理和监视变更数据捕获 (SQL Server)](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
