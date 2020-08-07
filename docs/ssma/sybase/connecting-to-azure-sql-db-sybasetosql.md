---
title: " (SybaseToSQL) 连接到 Azure SQL 数据库 |Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: a16ade8d212d3d197b858488dde05b439d8e989f
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864754"
---
# <a name="connecting-to-azure-sql-database-sybasetosql"></a>连接到 Azure SQL 数据库 (SybaseToSQL) 
若要将 Sybase 数据库迁移到 Azure SQL 数据库，必须连接到 Azure SQL 数据库的目标实例。 当你连接时，SSMA 将获取 Azure SQL 数据库实例中所有数据库的元数据，并在 Azure SQL 数据库元数据资源管理器中显示数据库元数据。 SSMA 存储连接到的 Azure SQL 数据库实例的信息，但不存储密码。  
  
连接到 Azure SQL 数据库将保持活动状态，直到关闭该项目。 重新打开项目时，如果需要与服务器建立活动连接，则必须重新连接到 Azure SQL 数据库。 在将数据库对象加载到 Azure SQL 数据库并迁移数据之前，可以脱机工作。  
  
有关 Azure SQL 数据库实例的元数据不会自动同步。 相反，若要更新 Azure SQL 数据库元数据资源管理器中的元数据，必须手动更新 Azure SQL 数据库元数据。 有关详细信息，请参阅本主题后面的 "同步 Azure SQL 数据库元数据" 一节。  
  
## <a name="required-azure-sql-database-permissions"></a>必需的 Azure SQL 数据库权限  
用于连接到 Azure SQL 数据库的帐户需要不同的权限，具体取决于该帐户执行的操作：  
  
1.  若要将 Sybase 对象转换为 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法、更新 AZURE Sql 数据库中的元数据，或者将转换的语法保存到脚本中，该帐户必须有权登录到 AZURE Sql 数据库的实例。  
  
2.  若要将数据库对象加载到 Azure SQL 数据库中，最低权限要求是目标数据库中**db_owner**数据库角色的成员身份。  
  
## <a name="establishing-an-azure-sql-database-connection"></a>建立 Azure SQL Database 连接  
在将 Sybase 数据库对象转换为 Azure SQL 数据库语法之前，必须建立与要迁移 Sybase 数据库的 Azure SQL 数据库实例的连接。  
  
定义连接属性时，还可以指定要将对象和数据迁移到的数据库。 连接到 Azure SQL 数据库后，可以在 Sybase 架构级别自定义此映射。 有关详细信息，请参阅[将 SYBASE ASE 架构映射到 SQL Server 架构 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> 尝试连接到 Azure SQL 数据库之前，请确保 Azure SQL 数据库的实例正在运行，并且可以接受连接。  
  
**连接到 Azure SQL 数据库**  
  
1.  在 "**文件**" 菜单上，选择 "**连接到 Azure SQL 数据库** (在创建项目) 后启用此选项。  
  
    如果以前已连接到 Azure SQL 数据库，则命令名称将**重新连接到 AZURE Sql 数据库**  
  
2.  在 "连接" 对话框中，输入或选择 Azure SQL 数据库的服务器名称。  
  
3.  输入，选择或**浏览**数据库名称。  
  
4.  输入或选择 "**用户名**"。  
  
5.  输入**密码**。  
  
6.  SSMA 建议对 Azure SQL 数据库进行加密连接。  
  
7.  单击“连接” 。  
  
> [!IMPORTANT]  
> 用于 Sybase 的 SSMA 不支持连接到 Azure SQL 数据库中的**master**数据库。  
  
## <a name="synchronizing-azure-sql-database-metadata"></a>同步 Azure SQL 数据库元数据  
有关 Azure SQL 数据库数据库的元数据不会自动更新。 Azure SQL 数据库元数据资源管理器中的元数据是首次连接到 Azure SQL 数据库时或上次手动更新元数据时的元数据的快照。 您可以为所有数据库或任何单个数据库或数据库对象手动更新元数据。  
  
**同步元数据**  
  
1.  请确保已连接到 Azure SQL 数据库。  
  
2.  在 Azure SQL 数据库 "元数据资源管理器" 中，选中要更新的数据库或数据库架构旁边的复选框。  
  
    例如，若要更新所有数据库的元数据，请选中 "数据库" 旁边的复选框。  
  
3.  右键单击 "数据库"、"数据库" 或 "数据库架构"，然后选择 "**与数据库同步**"。  
  
## <a name="next-step"></a>下一步  
迁移的下一步取决于你的项目需求：  
  
-   若要自定义 Sybase 架构与 Azure SQL 数据库与架构之间的映射，请参阅[将 SYBASE ASE 架构映射到 SQL Server 架构 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   若要自定义项目的配置选项，请参阅[设置项目选项 &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   若要自定义源和目标数据类型的映射，请参阅将[SYBASE ASE 和 SQL Server 数据类型映射 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   如果不需要执行这些任务中的任何一种，可以将 Sybase 数据库对象定义转换为 Azure SQL 数据库对象定义。 有关详细信息，请参阅将[SYBASE ASE 数据库对象转换 &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>另请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL 数据库 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
