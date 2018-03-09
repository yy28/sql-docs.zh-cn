---
title: "master 数据库 (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c71617c0-6689-4f52-81c6-58f4cf7c7377
caps.latest.revision: "8"
ms.workload: not set
ms.openlocfilehash: 1fde1a329703ed833a9fdeb6686b1a63c04aea79
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="master-database"></a>master 数据库
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
  
## <a name="related-tasks"></a>Related Tasks  
  
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
  
