---
title: 将 MySQL 数据库迁移到 SQL Server-Azure SQL 数据库 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8006f9a0-394d-4238-8dc5-44255134628b
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 33dd7faf67e82f1259ac87a0ef8e0eb5fdf2927d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908788"
---
# <a name="migrating-mysql-databases-to-sql-server---azure-sql-db-mysqltosql"></a>将 MySQL 数据库迁移到 SQL Server-Azure SQL DB (MySQLToSql)
SQL Server Migration Assistant (SSMA) for MySQL 是一个全面的环境，可帮助你快速将 MySQL 数据库迁移到 SQL Server 或 SQL Azure。 通过使用 SSMA for MySQL，可以查看数据库对象和数据、 评估要迁移的数据库，迁移到 SQL Server 或 SQL Azure 数据库对象并再将数据迁移到 SQL Server 或 SQL Azure。  
  
## <a name="recommended-migration-process"></a>建议的迁移过程  
若要成功迁移的对象和数据从 MySQL 数据库到 SQL Server 或 SQL Azure，请使用以下过程：  
  
1.  [处理 SSMA 项目&#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-ssma-projects-mysqltosql.md)。  
  
    创建项目后，可以设置项目转换、 迁移和类型映射选项。 有关项目设置的详细信息，请参阅[设置项目选项&#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)。 有关如何自定义数据类型映射的信息，请参阅[映射 MySQL 和 SQL Server 数据类型&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
2.  [连接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
3.  [连接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
4.  [将 MySQL 数据库映射到 SQL Server 架构&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
5.  [连接到 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
6.  （可选）[评估 MySQL 数据库以供转换&#40;MySQLToSQL&#41; ](../../ssma/mysql/assessing-mysql-databases-for-conversion-mysqltosql.md)评估转换数据库对象和估计的转换时间。  
  
7.  [转换 MySQL 数据库&#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
8.  [同步](loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
9. 可以通过以下方式之一执行此操作：  
  
    -   保存脚本和 SQL Server 或 SQL Azure 上运行。  
  
    -   同步数据库对象。  
  
10. [将 MySQL 数据迁移到 SQL Server-Azure SQL 数据库&#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
11. 如有必要，更新数据库应用程序。  
  
> [!NOTE]  
> 不能迁移 Information_schema 和 MySQL 架构。  
  
## <a name="see-also"></a>请参阅  
[安装 SSMA for MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
[开始使用 SSMA for MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)  
  
