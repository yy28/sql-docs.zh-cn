---
title: 需要已更新备份的常用操作 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], actions requiring a backup
- restoring [SQL Server replication], actions requiring a backup
- backups [SQL Server replication], actions requiring a backup
ms.assetid: a5975bf4-183e-42e3-b7d1-ad02f89d2e1d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 184bda56568cfcedbc07183bd2be7fdde7a789e4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52773229"
---
# <a name="common-actions-requiring-an-updated-backup"></a>需要已更新备份的常用操作
  如果执行定期日志备份，则在日志备份中应捕获所有与复制相关的更改。 如果不执行日志备份，就要在修改复制架构或拓扑之后，对发布、分发、订阅、 **msdb**数据库和 **master** 数据库执行备份。  
  
## <a name="publication-database"></a>发布数据库  
 在执行下列操作后备份发布数据库：  
  
-   创建新发布。  
  
-   更改包括筛选在内的任何发布属性。  
  
-   向现有发布中添加项目。  
  
-   在发布范围内重新初始化订阅。  
  
-   对已发布的表进行架构更改。  
  
-   使用 [sp_addscriptexec (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql) 按需执行脚本。  
  
-   更改任何项目属性。  
  
-   删除任何发布。  
  
-   删除任何项目。  
  
-   禁用复制。  
  
## <a name="distribution-database"></a>分发数据库  
 在执行下列操作后备份分发数据库：  
  
-   创建或修改复制代理配置文件。  
  
-   修改复制代理配置文件参数。  
  
-   更改任何推送订阅的复制代理属性（包括计划）。  
  
-   自动标识范围管理功能指定了新标识范围。  
  
## <a name="subscription-database"></a>订阅数据库  
 在执行下列操作后备份订阅数据库：  
  
-   更改任何订阅属性。  
  
-   在发布服务器上更改合并订阅的优先级。  
  
-   删除任何订阅。  
  
-   禁用复制。  
  
## <a name="msdb-database"></a>msdb 数据库  
 在执行下列操作后，在相应节点备份 **msdb** 系统数据库：  
  
-   启用或禁用复制。  
  
-   添加或删除分发数据库（在分发服务器上）。  
  
-   启用或禁用发布数据库（在发布服务器上）。  
  
-   创建或修改复制代理配置文件（在分发服务器上）。  
  
-   修改任何复制代理配置文件参数（在分发服务器上）。  
  
-   更改任何推送订阅的复制代理程序属性（包括计划）（在分发服务器上）。  
  
-   更改任何请求订阅的复制代理程序属性（包括计划）（在订阅服务器上）。  
  
-   创建与使用可转换订阅的事务发布相关联的 DTS 包（在分发服务器和订阅服务器上）。  
  
-   添加或删除可转换订阅（在分发服务器和订阅服务器上）。  
  
## <a name="master-database"></a>master 数据库  
 在执行下列操作后，在相应节点备份 **master** 系统数据库：  
  
-   启用或禁用复制。  
  
-   添加或删除分发数据库（在分发服务器上）。  
  
-   启用或禁用发布数据库（在发布服务器上）。  
  
-   在任何数据库中添加第一个发布或删除最后一个发布（在发布服务器上）。  
  
-   在任何数据库中添加第一个订阅或删除最后一个订阅（在订阅服务器上）。  
  
-   在分发发布服务器上启用或禁用发布服务器（在发布服务器和分发服务器上）。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 数据库的备份和还原](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [备份和还原复制的数据库](back-up-and-restore-replicated-databases.md)  
  
  
