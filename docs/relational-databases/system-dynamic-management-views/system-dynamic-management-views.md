---
title: 动态管理视图 (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database scoped dynamic management objects [SQL Server]
- dynamic management objects [SQL Server], about dynamic management objects
- server state information [SQL Server]
- dynamic management functions [SQL Server]
- metadata [SQL Server], dynamic management objects
- dynamic management views [SQL Server]
- DMVs [SQL Server]
- functions [SQL Server], dynamic management
- server scoped dynamic management objects [SQL Server]
- dynamic management objects [SQL Server]
ms.assetid: cf893ecb-0bf6-4cbf-ac00-8a1099e405b1
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7553cf42f79b16bfc49d494d4fe1861adc7b687b
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661706"
---
# <a name="system-dynamic-management-views"></a>系统动态管理视图
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  动态管理视图和函数返回可用于监视服务器实例的运行状况、诊断故障以及优化性能的服务器状态信息。  
  
> [!IMPORTANT]  
>  动态管理视图和函数返回特定于实现的内部状态数据。 在未来的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中，它们的架构和返回的数据可能会发生更改。 因此，未来版本中的动态管理视图和函数可能与此版本中的动态管理视图和函数不兼容。 例如，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未来版本中，Microsoft 可能会通过在列列表的末尾添加列来扩充任何动态管理视图的定义。 我们建议不要在生产代码中使用语法 `SELECT * FROM dynamic_management_view_name`，这是因为返回的列数可能会更改和中断应用程序。  
  
 动态管理视图和函数分为两种类型：  
  
-   服务器范围内的动态管理视图和函数。 此类型需要具有该服务器的 VIEW SERVER STATE 权限。  
  
-   数据库范围内的动态管理视图和函数。 此类型需要具有该数据库的 VIEW DATABASE STATE 权限。  
  
## <a name="querying-dynamic-management-views"></a>查询动态管理视图  
 通过使用两部分、三部分或四部分所组成的名称，可在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中引用动态管理视图。 另一方面，也可使用两部分或三部分所组成的名称在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中引用动态管理函数。 不能使用只由一部分组成的名称在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中引用动态管理视图和函数。  
  
 所有动态管理视图和函数都存在于 sys 架构中，并遵循 dm_* 命名约定。 当使用动态管理视图或函数时，必须使用 sys 架构作为视图或函数名称的前缀。 例如，若要查询 dm_os_wait_stats 动态管理视图，请运行以下查询：  
  
 ```sql
SELECT wait_type, wait_time_ms  
FROM sys.dm_os_wait_stats;  
```  
  
### <a name="required-permissions"></a>所需的权限  
 查询动态管理视图或函数需要对于对象具有 SELECT 权限以及 VIEW SERVER STATE 或 VIEW DATABASE STATE 权限。 这样您可以有选择地限制用户或登录名对动态管理视图和函数的访问。 为此，首先在 master 中创建用户，然后拒绝该用户对不希望被访问的动态管理视图或函数的 SELECT 权限。 此后，无论该用户的数据库上下文如何，用户都将无法选择这些动态管理视图或函数。  
  
> [!NOTE]  
>  由于 DENY 的优先级高，所以如果用户被授予 VIEW SERVER STATE 权限但被拒绝 VIEW DATABASE STATE 权限，则该用户只能查看服务器级别信息，但不能查看数据库级别信息。  
  
## <a name="in-this-section"></a>本节内容  
 动态管理视图和函数划分为以下类别。  
  
|||  
|-|-|  
|[Always On 可用性组动态管理视图和函数 (Transact SQL)](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)|[内存优化表动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)|  
|[与变更数据捕获相关的动态管理视图 (Transact-SQL)](https://msdn.microsoft.com/library/2a771d7d-693a-4f56-9227-02cd00e0e200)|[对象与相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[与更改跟踪相关的动态管理视图](https://msdn.microsoft.com/library/dc8a0af9-fcd8-4c34-9453-5132717c9bdb)|[查询通知相关的动态管理视图&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/92eb22d8-33f3-4c17-b32e-e23acdfbd8f4)|  
|[公共语言运行时与相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)|[与复制相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)|  
|[数据库镜像相关的动态管理视图&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/04fb21de-1b5e-4a8e-9ca6-1b78ad278db1)|[与资源调控器相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)|  
|[与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)|[与安全性相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[与执行相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)|[与服务器相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[扩展的事件动态管理视图](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)|[与 Service Broker 有关的动态管理视图 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)|  
|[Filestream 和 FileTable 动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)|[空间数据相关的动态管理视图和函数&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/c542ac38-451f-43a5-bf8c-4edd38bb738e)|  
|[全文搜索和语义搜索动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)|[SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)|  
|[异地复制动态管理视图和函数&#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)|[与 SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)|  
|[与索引相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)|[Stretch Database 的动态管理视图&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/1193efce-a105-49a9-a8b8-26b063485567)|  
|[我 O 相关动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)|[与事务相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)|  

  
## <a name="see-also"></a>请参阅  
 [GRANT 服务器权限&#40;Transact SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)   
 [GRANT 数据库权限 (Transact-SQL)](../../t-sql/statements/grant-database-permissions-transact-sql.md)   
 [系统视图&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
