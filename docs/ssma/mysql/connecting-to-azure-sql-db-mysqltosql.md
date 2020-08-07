---
title: " (MySQLToSQL) 连接到 Azure SQL 数据库 |Microsoft Docs"
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Azure, SQL Azure permissions
- Connecting to SQL Azure, synchronization
ms.assetid: d0b6f16a-1880-459d-a0c7-28b7ef15c56a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: da3e0d05abf24bdd7100769ecfbb597e2953a9d5
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87822556"
---
# <a name="connecting-to-azure-sql-database-mysqltosql"></a>连接到 Azure SQL 数据库 (MySQLToSQL) 
若要将 MySQL 数据库迁移到 SQL Azure，你必须连接到 SQL Azure 的目标实例。 在连接时，SSMA 将获取 SQL Azure 实例中所有数据库的元数据，并在 SQL Azure 元数据资源管理器中显示数据库元数据。 SSMA 存储连接到但不存储密码的 SQL Azure 实例的信息。  
  
到 SQL Azure 的连接保持活动状态，直到关闭项目。 重新打开项目时，如果需要与服务器建立活动连接，则必须重新连接到 SQL Azure。 在将数据库对象加载到 SQL Azure 和迁移数据之前，可以脱机工作。  
  
与 SQL Azure 实例有关的元数据不会自动同步。 相反，若要更新 SQL Azure 元数据资源管理器中的元数据，必须手动更新 SQL Azure 元数据。 有关详细信息，请参阅本主题后面的 "同步 SQL Azure 元数据" 一节。  
  
## <a name="required-sql-azure-permissions"></a>必需的 SQL Azure 权限  
用于连接 SQL Azure 的帐户需要不同的权限，具体取决于帐户执行的操作：  
  
-   若要将 MySQL 对象转换为 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法、从 SQL Azure 更新元数据，或者将转换的语法保存到脚本中，该帐户必须有权登录到 SQL Azure 实例。  
  
-   若要将数据库对象加载到 SQL Azure 中，最低权限要求是目标数据库中**db_owner**数据库角色的成员身份。  
  
## <a name="establishing-a-sql-azure-connection"></a>建立 SQL Azure 连接  
在将 MySQL 数据库对象转换为 SQL Azure 语法之前，必须与要迁移 MySQL 数据库的 SQL Azure 实例建立连接。  
  
定义连接属性时，还可以指定要将对象和数据迁移到的数据库。 连接到 SQL Azure 后，你可以在 MySQL 架构级别自定义此映射。 有关详细信息，请参阅[将 MySQL 数据库映射到 SQL Server 架构 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> 尝试连接到 SQL Azure 之前，请确保 SQL Azure 的实例正在运行，并且可以接受连接。  
  
**连接到 SQL Azure**  
  
1.  在 "**文件**" 菜单上，选择 "**连接到 SQL Azure** (在创建项目) 后启用此选项。  
  
    如果以前已连接到 SQL Azure，则命令名称将**重新连接到 SQL Azure**。  
  
2.  在 "连接" 对话框中，输入或选择 SQL Azure 的服务器名称。  
  
3.  输入，选择或**浏览**数据库名称。  
  
4.  输入或选择 "**用户名**"。  
  
5.  输入**密码**。  
  
6.  SSMA 建议将加密连接 SQL Azure。  
  
7.  单击“连接” 。  
  
> [!IMPORTANT]  
> SSMA for MySQL 不支持连接到 SQL Azure 中的**master**数据库。  
  
## <a name="synchronizing-sql-azure-metadata"></a>同步 SQL Azure 元数据  
不会自动更新与 SQL Azure 数据库有关的元数据。 SQL Azure 元数据资源管理器中的元数据是首次连接到 SQL Azure 或上次手动更新元数据时的元数据的快照。 您可以为所有数据库或任何单个数据库或数据库对象手动更新元数据。  
  
**同步元数据**  
  
1.  请确保已连接到 SQL Azure。  
  
2.  在 SQL Azure 元数据资源管理器 "中，选中要更新的数据库或数据库架构旁边的复选框。  
  
    例如，若要更新所有数据库的元数据，请选中 "数据库" 旁边的复选框。  
  
3.  右键单击 "数据库"、"数据库" 或 "数据库架构"，然后选择 "**与数据库同步**"。  
  
## <a name="next-step"></a>下一步  
迁移的下一步取决于你的项目需求：  
  
-   若要自定义 MySQL 架构与 SQL Azure 数据库和架构之间的映射，请参阅[将 Mysql 数据库映射到 SQL Server 架构 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   若要自定义项目的配置选项，请参阅[设置项目选项 &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   若要自定义源和目标数据类型的映射，请参阅[&#40;MySQLToSQL 映射 MySQL 和 SQL Server 数据类型&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   如果不需要执行这些任务中的任何一种，可以将 MySQL 数据库对象定义转换为 SQL Azure 对象定义。 有关详细信息，请参阅将[MySQL 数据库转换 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>另请参阅  
[将 MySQL 数据库迁移到 SQL Server-Azure SQL 数据库 &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
