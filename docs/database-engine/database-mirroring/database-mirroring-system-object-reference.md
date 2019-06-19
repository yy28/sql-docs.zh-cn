---
title: 数据库镜像系统对象参考 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 6f43477ebb45812fb4e71ca501296518ed3950c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795512"
---
# <a name="database-mirroring-system-object-reference"></a>数据库镜像系统对象参考
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="system-catalog-views"></a>系统目录视图

| 系统目录视图 | 描述|
| :------ | :----------------------------- |
| [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   | 服务器在数据库镜像合作关系中充当的每个见证服务器角色在表中都占用一行。 |
| &nbsp; | &nbsp; |

## <a name="system-dynamic-management-views"></a>系统动态管理视图

| 系统动态管理视图 | 描述|
| :------ | :----------------------------- |
| [sys.dm_db_mirroring_auto_page_repair](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-auto-page-repair.md)   | 对服务器实例上所有镜像数据库的每个自动页修复尝试返回一行。  |
| [sys.dm_db_mirroring_connections](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-connections.md)    | 针对为每个数据库镜像建立的连接返回一行。 |
| &nbsp; | &nbsp; |

## <a name="system-tables"></a>系统表

| 系统表 | 描述|
| :------ | :----------------------------- |
| [sysdbmaintplan_databases](../../relational-databases/system-tables/sysdbmaintplan-databases-transact-sql.md)   | 返回有关数据库镜像维护计划的信息。 |
| [sysdbmaintplan_history](../../relational-databases/system-tables/sysdbmaintplan-history-transact-sql.md)    | 返回有关数据库镜像维护计划的历史记录信息。 |
| [sysdbmaintplan_jobs](../../relational-databases/system-tables/sysdbmaintplan-jobs-transact-sql.md)    |返回有关数据库镜像维护计划作业的信息。  |
| [sysdbmaintplans](../../relational-databases/system-tables/sysdbmaintplans-transact-sql.md)    | 返回有关数据库镜像计划的信息。  |
| &nbsp; | &nbsp; |


## <a name="see-also"></a>另请参阅  
 [数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   

  
  
