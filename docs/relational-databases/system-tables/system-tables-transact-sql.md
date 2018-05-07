---
title: 系统表 (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server]
- tables [SQL Server], system tables
- information retrieval [SQL Server]
- status information [SQL Server], system tables
- system information [SQL Server]
- system tables [SQL Server]
- system tables [SQL Server], about system tables
- system tables [SQL Server], retrieving information from
- retrieving system table information
ms.assetid: 56b8ad51-930c-4e5c-8d99-8c939d5b70ac
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2658b6ab0687a3eb3c63d6d658f93ff2c25b55c6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="system-tables-transact-sql"></a>系统表 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本节中的主题介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的系统表。  
  
 任何用户都不应直接更改系统表。 例如，不要尝试使用 DELETE、UPDATE、INSERT 语句或用户定义的触发器修改系统表。  
  
 允许在系统表中引用所记录的列。 然而，系统表中的许多列都未被记录。 不应编写应用程序直接查询未记录的列。 相反，若要检索存储在系统表中的信息，应用程序应使用下列组件之一：  
  
-   系统存储过程  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句和函数  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象 (SMO)  
  
-   复制管理对象 (RMO)  
  
-   数据库 API 目录函数  
  
 这些组件构成一个已发布的 API，用以从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 获取系统信息。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 维护这些组件在不同版本间的兼容性。 系统表的格式取决于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的内部体系结构，并且可能因不同的版本而异。 因此，直接访问系统表中未记录列的应用程序可能需要进行更改，然后才能访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的更高版本。  
  
## <a name="in-this-section"></a>本節內容  
 系统表主题按下列功能范围进行组织：  
  
|||  
|-|-|  
|[备份和还原表&#40;Transact SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)|[日志传送表 (Transact-SQL)](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)|  
|[更改数据捕获表&#40;Transact SQL&#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)|[复制表 (Transact-SQL)](../../relational-databases/system-tables/replication-tables-transact-sql.md)|  
|[数据库维护计划表&#40;Transact SQL&#41;](../../relational-databases/system-tables/database-maintenance-plan-tables-transact-sql.md)|[SQL Server 代理表&#40;Transact SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)|  
|[SQL Server 扩展事件表&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/6d52ff03-f5aa-4f0f-8c98-9b49dc76f94e)|[sys.sysoledbusers &#40;Transact SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysoledbusers-transact-sql.md)|  
|[Integration Services 表&#40;Transact SQL&#41;](../../relational-databases/system-tables/integration-services-tables-transact-sql.md)|[systranschemas &#40;Transact SQL&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)|  
  
## <a name="see-also"></a>另请参阅  
 [兼容性视图&#40;Transact SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
