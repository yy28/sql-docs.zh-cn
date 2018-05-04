---
title: 将 MySQL 数据库迁移到 SQL Server 的 Azure SQL DB |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8006f9a0-394d-4238-8dc5-44255134628b
caps.latest.revision: 12
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 771b28d558c9f34e1e41934ba6837678ee8b2415
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="migrating-mysql-databases-to-sql-server---azure-sql-db-mysqltosql"></a>将 MySQL 数据库迁移到 SQL Server 的 Azure SQL DB (MySQLToSql)
SQL Server 迁移助手 (SSMA) mysql 是一个全面的环境，可帮助你快速将 MySQL 数据库迁移到 SQL Server 或 SQL Azure。 通过使用面向 MySQL 的 SSMA，你可以查看数据库对象和数据、 评估迁移的数据库，迁移到 SQL Server 或 SQL Azure 的数据库对象，然后将数据迁移到 SQL Server 或 SQL Azure。  
  
## <a name="recommended-migration-process"></a>建议迁移过程  
若要成功迁移对象和数据从 MySQL 数据库到 SQL Server 或 SQL Azure，请使用以下过程：  
  
1.  [使用 SSMA 项目&#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-ssma-projects-mysqltosql.md)。  
  
    创建项目后，你可以设置项目转换、 迁移和类型映射选项。 有关项目设置的详细信息，请参阅[设置项目选项&#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)。 有关如何自定义数据类型映射的信息，请参阅[映射 MySQL 和 SQL Server 数据类型&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
2.  [连接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
3.  [连接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
4.  [将 MySQL 数据库映射到 SQL Server 架构&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
5.  [连接到 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
6.  （可选）[评估 MySQL 数据库以供转换&#40;MySQLToSQL&#41; ](../../ssma/mysql/assessing-mysql-databases-for-conversion-mysqltosql.md)以评估转换的数据库对象，并估计转换时间。  
  
7.  [将 MySQL 数据库转换&#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
8.  [同步](http://msdn.microsoft.com/en-us/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
9. 可以通过以下方式之一来执行此操作：  
  
    -   保存脚本，并在 SQL Server 或 SQL Azure 上运行它。  
  
    -   同步数据库对象。  
  
10. [将 MySQL 数据迁移到 SQL Server 的 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
11. 如有必要，更新数据库应用程序。  
  
> [!NOTE]  
> 您无法迁移 Information_schema 和 MySQL 的架构。  
  
## <a name="see-also"></a>另请参阅  
[安装适用于 MySQL SSMA &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
[入门 MySQL SSMA &#40;MySQLToSQL&#41;](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)  
  
