---
title: Master 数据库的并行数据仓库 |Microsoft 文档
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
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="master-database---parallel-data-warehouse"></a>Master 数据库的并行数据仓库
SQL Server PDW master 数据库存储设备级别登录名信息和数据库目录。 它是控制节点驻留的 SQL Server master 数据库。 在这种情况下，它提供类似的功能到 SQL Server PDW 像 master 提供到 SQL Server。  
  
有关系统数据库的详细信息，请参阅[系统数据库](system-databases.md)。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
以下列表描述不能对 SQL Server PDW master 数据库执行的操作。  
  
你*不能：*  
  
-   执行 master 的差异备份。  
  
-   在 master 中创建用户对象。  
  
-   更改 master 数据库的排序规则。  
  
-   更改 master 数据库的所有者。  
  
-   删除或重命名母版。  
  
-   修改主机的权限。  
  
-   执行**DBCC SHRINKLOG**。  
  
## <a name="related-tasks"></a>相关任务  
  
|任务|Description|  
|--------|---------------|  
|创建 master 的完整备份。|例如：<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />有关详细信息，请参阅[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)。|  
|还原 master 数据库|若要还原的 master 数据库，使用[还原 Master 数据库](restore-the-master-database.md)Configuration Manager 工具页中的。|  
|查看数据库目录信息。|`SELECT * FROM master.sys.databases;`|  
|查看系统级登录名和权限信息。|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
