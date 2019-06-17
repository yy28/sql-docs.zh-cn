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
manager: craigg
ms.openlocfilehash: ac8b97e36338a280b6f78a0e6bb73eeab882655d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63297474"
---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>连接到 Azure SQL DB (SybaseToSQL)
将 Sybase 数据库迁移到 Azure SQL DB，必须连接到 Azure SQL DB 的目标实例。 连接时，SSMA 获取有关 Azure SQL 数据库实例中的所有数据库的元数据，并在 Azure SQL DB 元数据资源管理器中显示数据库元数据。 SSMA 存储的 Azure SQL DB 连接到，但不存储密码的实例的信息。  
  
与 Azure SQL DB 的连接保持活动状态，直到关闭该项目。 当你重新打开该项目时，你必须重新连接到 Azure SQL DB 中，如果想要的活动连接到服务器。 将数据库对象加载到 Azure SQL 数据库并迁移数据之前，您可以脱机工作。  
  
有关 Azure SQL DB 实例的元数据不会自动同步。 相反，若要更新 Azure SQL DB 元数据资源管理器中的元数据，必须手动更新 Azure SQL DB 元数据。 有关详细信息，请参阅本主题后面的"同步 Azure SQL DB 元数据"部分。  
  
## <a name="required-azure-sql-db-permissions"></a>所需的 Azure SQL DB 权限  
用于连接到 Azure SQL DB 的帐户需要不同的权限，具体取决于该帐户执行的操作：  
  
1.  要转换到 Sybase 对象[!INCLUDE[tsql](../../includes/tsql-md.md)]语法中，更新元数据从 Azure SQL DB，或将保存到转换后的语法编写的脚本，该帐户必须有权登录到 Azure SQL DB 的实例。  
  
2.  若要将数据库对象加载到 Azure SQL DB，最小权限要求是中的成员身份**db_owner**目标数据库中的数据库角色。  
  
## <a name="establishing-a-azure-sql-db-connection"></a>建立一个 Azure SQL DB 连接  
将 Sybase 数据库对象转换为 Azure SQL DB 语法之前，必须建立与想要迁移的 Sybase 数据库的 Azure SQL DB 的实例的连接。  
  
在定义的连接属性时，还可以指定对象和数据将迁移的数据库。 连接到 Azure SQL DB 后，可以自定义此映射 Sybase 架构级别上。 有关详细信息，请参阅[到 SQL Server 架构映射 Sybase ASE 架构&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> 尝试连接到 Azure SQL 数据库之前，请确保 Azure SQL DB 的实例正在运行，并且可以接受连接。  
  
**若要连接到 Azure SQL DB**  
  
1.  上**文件**菜单中，选择**连接到 Azure SQL DB**（在创建项目后启用此选项）。  
  
    如果你之前已连接到 Azure SQL DB，命令名称将为**重新连接到 Azure SQL DB**  
  
2.  在连接对话框中，输入或选择 Azure SQL DB 服务器名称。  
  
3.  输入中，选择或**浏览**数据库名称。  
  
4.  输入或选择**用户名**。  
  
5.  输入**密码**。  
  
6.  SSMA 建议加密的连接到 Azure SQL DB。  
  
7.  单击 **“连接”** 。  
  
> [!IMPORTANT]  
> 适用于 Sybase 的 SSMA 不支持连接到**主**Azure SQL DB 中的数据库。  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>同步 Azure SQL DB 元数据  
有关 Azure SQL DB 数据库的元数据不会自动更新。 首次连接到 Azure SQL DB 或您手动更新元数据的最后一个时间时，Azure SQL DB 元数据资源管理器中的元数据是元数据的快照。 您可以手动更新所有数据库，或任何单个数据库或数据库对象的元数据。  
  
**同步元数据**  
  
1.  请确保你已连接到 Azure SQL DB。  
  
2.  在 Azure SQL DB 元数据资源管理器中，选择你想要更新的数据库架构的数据库旁边的复选框。  
  
    例如，若要更新的所有数据库的元数据，请选择数据库旁边的框。  
  
3.  右键单击数据库，或单个数据库或数据库架构，然后选择**与数据库同步**。  
  
## <a name="next-step"></a>下一步  
迁移的下一步取决于您的项目需求：  
  
-   若要自定义 Sybase 架构和 Azure SQL DB 数据库和架构之间的映射，请参阅[Sybase ASE 架构映射到 SQL Server 架构&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   若要自定义项目的配置选项，请参阅[设置项目选项&#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   若要自定义源和目标数据类型的映射，请参阅[映射 Sybase ASE 和 SQL Server 数据类型&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   如果不需要执行任何这些任务，可以将 Sybase 数据库对象定义转换到 Azure SQL DB 对象定义。 有关详细信息，请参阅[转换 Sybase ASE 数据库对象&#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
