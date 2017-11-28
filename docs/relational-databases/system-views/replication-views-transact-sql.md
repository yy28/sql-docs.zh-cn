---
title: "复制视图 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: TSQL
helpviewer_keywords:
- distribution databases [SQL Server replication], system views
- metadata [SQL Server], views
- views [SQL Server], replication
- replication views [SQL Server]
- publications [SQL Server replication], system views
- articles [SQL Server replication], system views
- replication metadata [SQL Server]
- subscriptions [SQL Server replication], system views
- system views [SQL Server], replication
ms.assetid: 93e5056d-0d93-4a48-ba33-72762eb995d8
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b73dfed7709b76d20856fe03648a7e0c6db0d258
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="replication-views-transact-sql"></a>复制视图 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  这些视图包含中的复制将使用的信息[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 视图启用中的数据容易访问[复制系统表](../../relational-databases/system-tables/replication-tables-transact-sql.md)。 将某个用户数据库启用为发布数据库或订阅数据库时，便会在该数据库中创建视图。 从复制拓扑中删除用户数据库时，便会删除该数据库中的所有复制对象。 用于访问复制元数据的首选的方法是通过使用[复制存储过程](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。  
  
> [!IMPORTANT]  
>  任何用户都不应直接更改系统视图。  
  
## <a name="replication-views"></a>复制视图  
 以下是复制所使用的系统视图的列表（按数据库分组）。  
  
### <a name="replication-views-in-the-msdb-database"></a>msdb 数据库中的复制视图  
  
|||  
|-|-|  
|[MSdatatype_mappings &#40;Transact SQL &#41;](../../relational-databases/system-views/msdatatype-mappings-transact-sql.md)|[sysdatatypemappings &#40;Transact SQL &#41;](../../relational-databases/system-views/sysdatatypemappings-transact-sql.md)|  
  
### <a name="replication-views-in-the-distribution-database"></a>分发数据库中的复制视图  
  
|||  
|-|-|  
|[IHextendedArticleView &#40;Transact SQL &#41;](../../relational-databases/system-views/ihextendedarticleview-transact-sql.md)|[sysarticles &#40;系统视图 &#41;&#40;Transact SQL &#41;](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)|  
|[IHextendedSubscriptionView &#40;Transact SQL &#41;](../../relational-databases/system-views/ihextendedsubscriptionview-transact-sql.md)|[sysextendedarticlesview &#40;Transact SQL &#41;](../../relational-databases/system-views/sysextendedarticlesview-transact-sql.md)|  
|[IHsyscolumns &#40;Transact SQL &#41;](../../relational-databases/system-views/ihsyscolumns-transact-sql.md)|[syspublications（系统视图）&#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)|  
|[MSdistribution_status &#40;Transact SQL &#41;](../../relational-databases/system-views/msdistribution-status-transact-sql.md)|[syssubscriptions（系统视图）&#40;Transact-SQL&#41;](../../relational-databases/system-views/syssubscriptions-system-view-transact-sql.md)|  
|[sysarticlecolumns &#40;系统视图 &#41;&#40;Transact SQL &#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)||  
  
### <a name="replication-views-in-the-publication-database"></a>发布数据库中的复制视图  
  
|||  
|-|-|  
|[sysmergeextendedarticlesview &#40;Transact SQL &#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[sysmergepartitioninfoview &#40;Transact SQL &#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[systranschemas &#40;Transact SQL &#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
### <a name="replication-views-in-the-subscription-database"></a>订阅数据库中的复制视图  
  
|||  
|-|-|  
|[sysmergeextendedarticlesview &#40;Transact SQL &#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[sysmergepartitioninfoview &#40;Transact SQL &#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[systranschemas &#40;Transact SQL &#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
## <a name="see-also"></a>另请参阅  
 [复制表 (Transact-SQL)](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
