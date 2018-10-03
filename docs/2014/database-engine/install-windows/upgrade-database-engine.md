---
title: 升级数据库引擎 | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4767b695f0c2c3668278e30f47f389664b4a4ef0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189547"
---
# <a name="upgrade-database-engine"></a>升级数据库引擎
  本主题提供了为升级过程进行准备和了解升级过程所需的信息，其中包括：  
  
-   已知升级问题。  
  
-   升级前的任务和注意事项。  
  
-   有关升级 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的过程主题的链接。  
  
-   将数据库迁移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的过程主题的链接。  
  
-   故障转移群集的注意事项。  
  
-   升级后的任务和注意事项。  
  
## <a name="known-upgrade-issues"></a>已知升级问题  
 升级 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 之前，请查看 [SQL Server 数据库引擎的向后兼容性](../sql-server-database-engine-backward-compatibility.md)。 有关支持的升级方案和已知升级问题的信息，请参阅[支持的版本升级](supported-version-and-edition-upgrades.md)。 有关其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件的向后兼容性的内容，请参阅[向后兼容性](../../getting-started/backward-compatibility.md)。  
  
> [!IMPORTANT]  
>  在从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的某一版本升级到另一版本之前，请验证要升级到的版本是否支持当前使用的功能。  
  
> [!NOTE]  
>  在从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise 版的之前版本升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，在“Enterprise Edition：基于内核授予许可”和 Enterprise Edition 之间进行选择。 这些 Enterprise 版本仅在许可模式方面存在不同。 有关详细信息，请参阅 [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
  
## <a name="pre-upgrade-checklist"></a>升级准备一览表  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序支持从早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进行升级。 也可以迁移早期 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中的数据库。 可以从一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例迁移至同一台计算机上的另一个实例，也可以从另一台计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例迁移。 迁移选项包括使用复制数据库向导、 备份和还原功能，利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]导入和导出向导中，以及批量导出/批量导入方法。  
  
 升级 [!INCLUDE[ssDE](../../includes/ssde-md.md)]之前，请先查看以下主题：  
  
-   阅读 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。  
  
-   阅读 [Check Parameters for the System Configuration Checker](check-parameters-for-the-system-configuration-checker.md)。  
  
-   阅读 [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)。  
  
-   查看[支持的版本升级](supported-version-and-edition-upgrades.md)。  
  
-   查看[使用升级顾问来准备升级](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)。  
  
-   查看[使用分布式重播实用工具准备升级](../../sql-server/install/use-the-distributed-replay-utility-to-prepare-for-upgrades.md)。  
  
-   查看 [SQL Server 数据库引擎的向后兼容性](../sql-server-database-engine-backward-compatibility.md)。  
  
-   查看[迁移查询计划](change-the-database-compatibility-mode-and-use-the-query-store.md)。  
  
 请在升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前检查下列问题并做出更改：  
  
-   当升级在 MSX/TSX 关系中登记了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，应在升级主服务器之前升级目标服务器。 如果您在升级目标服务器之前升级主服务器，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将无法连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的主实例。  
  
-   从 64 位版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升级到 64 位版本的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 时，必须先升级 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，再升级 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
-   如有必要，请备份要升级的实例中的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库文件，以便可以还原这些文件。  
  
-   在要升级的数据库上运行适当的数据库控制台命令 (DBCC)，以确保这些数据库处于一致状态。  
  
-   估计升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件以及用户数据库所需的磁盘空间。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件所需磁盘空间的信息，请参阅[安装 SQL Server 2014 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。  
  
-   确保将现有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据库（master、model、msdb 和 tempdb）配置为自动增长，并确保它们具有足够的硬盘空间。  
  
-   确保所有数据库服务器的 master 数据库中都有登录信息。 这对还原数据库很重要，因为 master 数据库中有系统登录信息。  
  
-   禁用所有启动存储过程，因为升级过程在升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时将停止然后再启动服务。 在启动时进行处理的存储过程可能会阻塞升级过程。  
  
-   确保复制正在进行，然后停止复制。  
  
-   退出所有应用程序，包括所有依赖 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的服务。 如果有本地应用程序连接到要升级的实例，则升级可能会失败。  
  
-   如果使用数据库镜像，请参阅[在升级服务器实例时最大限度地减少镜像数据库的停机时间](../database-mirroring/upgrading-mirrored-instances.md)。  
  
## <a name="upgrading-the-database-engine"></a>升级数据库引擎  
 可以用升级版本覆盖 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本的安装。 如果在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序时检测到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本，将升级所有早期 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程序文件，并且保留早期 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中存储的所有数据。 此外，计算机上早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书将保持不变。  
  
> [!WARNING]  
>  运行 SQL Server 2014 安装程序时，作为运行预升级检查的一部分，将停止并重启 SQL Server 实例。  
  
> [!CAUTION]  
>  在升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 后，早期的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例将被覆盖，在计算机中不再存在。 因此在升级前，请备份 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库以及与早期的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例相关的其他对象。  
  
 可以使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 安装向导升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
### <a name="database-compatibility-level-after-upgrade"></a>升级后的数据库兼容级别  
 兼容性级别`tempdb`， `model`，`msdb`并**资源**升级后的数据库将设置为 120。 `master` 系统数据库保留它在升级之前的兼容级别。  
  
 如果升级前用户数据库的兼容级别为 100 或更高，升级后将保持相应级别。 如果升级前兼容级别为 90，则在升级后的数据库中，兼容级别将设置为 100，该级别为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]支持的最低兼容级别。  
  
> [!NOTE]  
>  新的用户数据库将继承的兼容性级别`model`数据库。  
  
## <a name="migrating-databases"></a>迁移数据库  
 可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的备份和还原功能或分离和附加功能将用户数据库移动到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 有关详细信息，请参阅[通过备份和还原来复制数据库](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)或[数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)。  
  
> [!IMPORTANT]  
>  数据库在源服务器和目的服务器上的名称相同时，不能进行移动或复制。 在这种情况下，它被标记为“已存在”。  
  
 有关更多信息，请参见 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="after-upgrading-the-database-engine"></a>升级数据库引擎后  
 升级 [!INCLUDE[ssDE](../../includes/ssde-md.md)]后，请完成以下任务：  
  
-   重新注册服务器。 有关注册服务器的详细信息，请参阅[注册服务器](../../ssms/register-servers/register-servers.md)。  
  
-   重新填充全文目录以便确保查询结果中的语义一致性。  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 将安装新的断字符以供全文和语义搜索使用。 在建立索引时和查询时均使用断字符。 如果您没有重新生成全文目录，搜索结果可能不一致。 如果您发出查找某一短语的全文查询和当前断字符，该短语是由以前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中的断字符以不同方式进行断字的，则可能不会检索包含该短语的文档或行。 其原因在于，建立了索引的短语是使用与正使用的查询不同的逻辑进行断字的。 解决方法是使用新的断字符来重新填充（重新生成）全文目录，以便索引时行为和查询时行为完全相同。  
  
     有关详细信息，请参阅 [sp_fulltext_catalog (Transact SQL)](/sql/relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql)。  
  
-   配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装。 为了减少系统的可攻击外围应用， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 有选择地安装和启用了一些关键服务和功能。  
  
-   验证或删除 USE PLAN 提示，这些提示由 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 生成并应用于对已分区表和索引的查询。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更改对已分区的表和索引的查询处理的方式。 如果已分区对象将 USE PLAN 提示用于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 生成的计划，针对这些对象的查询可能会包含不可在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中使用的计划。 建议升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]后，执行下列过程。  
  
     **如果直接在查询中指定 USE PLAN 提示：**  
  
    1.  从查询删除 USE PLAN 提示。  
  
    2.  测试查询。  
  
    3.  如果优化器未选择相应的计划并优化查询，请考虑使用所需的查询计划指定 USE PLAN 提示。  
  
     **如果计划指南中指定 USE PLAN 提示：**  
  
    1.  使用 sys.fn_validate_plan_guide 函数来检查计划指南的有效性。 或者，可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]中的 Plan Guide Unsuccessful 事件检查是否存在无效计划。  
  
    2.  如果计划指南无效，则删除该计划指南。 如果优化器未选择相应的计划并优化查询，则考虑使用所需查询计划指定 USE PLAN 提示。  
  
     当在计划指南中指定 USE PLAN 提示时，无效的计划将不会导致查询失败。 相反，仍可在不使用 USE PLAN 提示的情况下对计划进行编译。  
  
 在升级前标记为启用或禁用全文的数据库，在升级后也将保持该状态。 升级后，将为所有启用全文的数据库自动重新生成并填充全文目录。 此项操作既耗时又耗费资源。 可以通过运行以下语句暂停全文索引操作：  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 1;  
```  
  
 若要恢复全文检索填充，请运行以下语句：  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 0;  
```  
  
## <a name="see-also"></a>请参阅  
 [支持的版本升级](supported-version-and-edition-upgrades.md)   
 [使用多个版本和 SQL Server 的实例](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)   
 [后向兼容性](../../getting-started/backward-compatibility.md)   
 [升级复制的数据库](upgrade-replicated-databases.md)  
  
  
