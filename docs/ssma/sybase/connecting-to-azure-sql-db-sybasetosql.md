---
title: 连接到 Azure SQL DB (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 10be1dc3652c944b9de08a01b0f4cdff5ae5849a
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176237"
---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>连接到 Azure SQL DB (SybaseToSQL)
若要将 Sybase 数据库迁移到 Azure SQL DB, 必须连接到 Azure SQL 数据库的目标实例。 当你连接时, SSMA 将获取 Azure SQL 数据库实例中所有数据库的元数据, 并在 Azure SQL DB 元数据资源管理器中显示数据库元数据。 SSMA 存储您连接到的 Azure SQL DB 实例的信息, 但不存储密码。  
  
连接到 Azure SQL DB 会保持活动状态, 直到关闭项目。 重新打开项目时, 如果需要与服务器建立活动连接, 则必须重新连接到 Azure SQL DB。 在将数据库对象加载到 Azure SQL DB 并迁移数据之前, 可以脱机工作。  
  
有关 Azure SQL 数据库实例的元数据不会自动同步。 相反, 若要更新 Azure SQL 数据库元数据资源管理器中的元数据, 必须手动更新 Azure SQL 数据库元数据。 有关详细信息, 请参阅本主题后面的 "同步 Azure SQL DB 元数据" 一节。  
  
## <a name="required-azure-sql-db-permissions"></a>必需的 Azure SQL DB 权限  
用于连接到 Azure SQL DB 的帐户需要不同的权限, 具体取决于该帐户执行的操作:  
  
1.  若要将 Sybase 对象[!INCLUDE[tsql](../../includes/tsql-md.md)]转换为语法、更新 azure sql 数据库中的元数据, 或将转换后的语法保存到脚本中, 该帐户必须具有登录到 azure sql db 实例的权限。  
  
2.  若要将数据库对象加载到 Azure SQL DB 中, 最低权限要求是目标数据库中的**db_owner**数据库角色的成员身份。  
  
## <a name="establishing-an-azure-sql-db-connection"></a>建立 Azure SQL DB 连接  
在将 Sybase 数据库对象转换为 Azure SQL DB 语法之前, 必须建立与要在其中迁移 Sybase 数据库的 Azure SQL 数据库实例的连接。  
  
定义连接属性时, 还可以指定要将对象和数据迁移到的数据库。 连接到 Azure SQL DB 后, 可以在 Sybase 架构级别自定义此映射。 有关详细信息, 请参阅[将 SYBASE ASE 架构映射到&#40;SQL Server&#41;架构 SybaseToSQL](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> 尝试连接到 Azure SQL 数据库之前, 请确保 Azure SQL DB 的实例正在运行, 并且可以接受连接。  
  
**连接到 Azure SQL DB**  
  
1.  在 "**文件**" 菜单上, 选择 "**连接到 Azure SQL DB**" (此选项在创建项目后启用)。  
  
    如果以前已连接到 Azure SQL DB, 则命令名称将**重新连接到 AZURE SQL db**  
  
2.  在 "连接" 对话框中, 输入或选择 Azure SQL 数据库的服务器名称。  
  
3.  输入, 选择或**浏览**数据库名称。  
  
4.  输入或选择 "**用户名**"。  
  
5.  输入**密码**。  
  
6.  SSMA 建议将加密连接到 Azure SQL DB。  
  
7.  单击 **“连接”** 。  
  
> [!IMPORTANT]  
> 用于 Sybase 的 SSMA 不支持连接到 Azure SQL DB 中的**master**数据库。  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>同步 Azure SQL DB 元数据  
有关 Azure SQL DB 数据库的元数据不会自动更新。 Azure SQL DB 元数据资源管理器中的元数据是首次连接到 Azure SQL DB 或上次手动更新元数据时的元数据的快照。 您可以为所有数据库或任何单个数据库或数据库对象手动更新元数据。  
  
**同步元数据**  
  
1.  请确保已连接到 Azure SQL DB。  
  
2.  在 Azure SQL DB "元数据资源管理器" 中, 选中要更新的数据库或数据库架构旁边的复选框。  
  
    例如, 若要更新所有数据库的元数据, 请选中 "数据库" 旁边的复选框。  
  
3.  右键单击 "数据库"、"数据库" 或 "数据库架构", 然后选择 "**与数据库同步**"。  
  
## <a name="next-step"></a>下一步  
迁移的下一步取决于你的项目需求:  
  
-   若要自定义 Sybase 架构与 Azure SQL 数据库与架构之间的映射, 请参阅[将 SYBASE ASE 架构映射&#40;到&#41; SQL Server 架构 SybaseToSQL](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   若要自定义项目的配置选项, 请参阅[设置&#40;项目&#41;选项 SybaseToSQL](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   若要自定义源和目标数据类型的映射, 请参阅[映射 SYBASE ASE 和 SQL Server &#40;数据&#41;类型 SybaseToSQL](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   如果不需要执行这些任务中的任何一种, 可以将 Sybase 数据库对象定义转换为 Azure SQL DB 对象定义。 有关详细信息, 请参阅[转换 SYBASE ASE 数据库&#40;对象&#41; SybaseToSQL](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL &#40;DB SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
