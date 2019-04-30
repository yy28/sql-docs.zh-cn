---
title: Master 数据库的并行数据仓库 |Microsoft Docs
description: 了解有关并行数据仓库中的 master 数据库。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: bf07b9c27e08a49cb0866b177a0ec37fed4528a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213300"
---
# <a name="master-database---parallel-data-warehouse"></a>Master 数据库的并行数据仓库
SQL Server PDW 主数据库存储设备级登录名的信息和数据库目录。 它是 SQL Server master 数据库驻留在控制节点上。 在这种情况下，它提供类似的功能为 SQL Server PDW 如 master 提供对 SQL Server。  
  
系统数据库的详细信息，请参阅[系统数据库](system-databases.md)。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
以下列表描述不能对 SQL Server PDW master 数据库执行的操作。  
  
您*不能：*  
  
-   执行 master 的差异备份。  
  
-   在 master 中创建用户对象。  
  
-   更改主节点的排序规则。  
  
-   更改主节点的所有者。  
  
-   删除或重命名主机。  
  
-   修改主机的权限。  
  
-   执行**DBCC SHRINKLOG**。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务|描述|  
|--------|---------------|  
|创建主节点的完整备份。|例如：<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />有关详细信息，请参阅[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)。|  
|还原 master 数据库|若要还原 master 数据库，请使用[还原 Master 数据库](restore-the-master-database.md)配置管理器工具中的页。|  
|查看数据库目录信息。|`SELECT * FROM master.sys.databases;`|  
|查看整个系统的登录名和权限信息。|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
