---
title: 使用 SSMA 项目 (MySQLToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 32018a99e3bd376aa5d80df2c24c27a1aa341ec9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="working-with-ssma-projects-mysqltosql"></a>使用 SSMA 项目 (MySQLToSQL)
若要将 MySQL 数据库迁移到 SQL Server 或 SQL Azure，必须首先创建的 SSMA 项目。 项目是一个文件，其中包含以下信息：  
  
-   你想要迁移到 SQL Server 或 SQL Azure 的 MySQL 数据库的相关元数据。  
  
-   有关 SQL Server 或 SQL Azure 将接收迁移的对象和数据的目标实例元数据。  
  
-   SQL Server 或 SQL Azure 连接信息。  
  
-   项目设置。  
  
当你打开的项目时，它从 MySQL 和 SQL Server 或 SQL Azure 中断开。 允许您在脱机工作。 有关重新连接到 SQL Server 的详细信息，请参阅[连接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="reviewing-default-project-settings"></a>查看默认项目设置  
SSMA 进行转换和加载数据库、 迁移数据，和与 MySQL 和 SQL Server 或 SQL Azure 同步 SSMA 包含多个设置。 默认设置是适用于多个用户。 但是，在创建新的 SSMA 项目之前，你应查看这些设置。 如果需要，你可以更改将用于所有新项目的默认设置。  
  
##### <a name="to-review-default-project-settings"></a>若要查看默认项目设置  
  
1.  选择**默认项目设置**从**工具**菜单。  
  
2.  选择中的项目类型**迁移目标版本**下拉列表的设置是查看 / 更改，然后单击**常规**选项卡。  
  
3.  在左窗格中，单击**转换**。  
  
4.  在右窗格中，查看并根据需要更改设置。 有关这些设置的详细信息，请参阅[项目设置&#40;转换&#41; &#40;MySQLToSQL&#41; ](../../ssma/mysql/project-settings-conversion-mysqltosql.md) 。  
  
5.  重复步骤 1-3 的迁移、 同步、 SQL Azure、 GUI，和类型映射页。  
  
-   有关迁移设置的信息，请参阅[项目设置&#40;迁移&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)。  
  
-   有关 SQL Server 的同步设置的信息，请参阅[项目设置&#40;同步&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)。  
  
-   有关 GUI 设置的信息，请参阅[项目设置 (GUI) （SSMA 常见）](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
-   有关数据类型映射设置的信息，请参阅[项目设置&#40;类型映射&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)。  
  
-   有关 SQL Azure 设置信息，请参阅[项目设置&#40;Azure SQL DB&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)。  
  
> [!NOTE]  
> 仅当你选择时，将显示 SQL Azure 设置**迁移到 SQL Azure**在创建项目。  
  
## <a name="creating-new-projects"></a>创建新项目  
若要将数据从 MySQL 数据库迁移到 SQL Server 或 SQL Azure，必须创建一个项目。  
  
##### <a name="to-create-a-new-project"></a>创建新项目的步骤  
  
1.  选择**新项目**从**文件**菜单。 此时将显示“新建项目”  对话框。 在“文件”菜单中，选择“新建项目”。 此时将显示“新建项目”  对话框。  
  
2.  在**名称**框中，输入你的项目的名称。  
  
3.  在**位置**框中，输入或选择用于项目的文件夹。  
  
4.  在**迁移到**下拉列表中，选择的目标版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]用于迁移。 可用选项包括：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   Azure SQL 数据库  
  
然后单击**确定**  
  
SSMA 创建项目文件。  
  
## <a name="customizing-project-settings"></a>自定义项目设置  
除了定义默认值应用于所有新的 SSMA 项目的项目设置还可以自定义的每个项目的设置。 有关详细信息，请参阅[设置项目选项&#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)。  
  
当你自定义源和目标数据库之间的数据类型映射时，你可以定义在项目、 数据库或对象级别的映射。 有关详细信息，请参阅[映射 MySQL 和 SQL Server 数据类型&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)。  
  
## <a name="saving-projects"></a>保存项目  
保存项目功能允许用户将实质上是 SSMA 项目文件中保存项目设置和数据库元数据 （可选）。  
  
##### <a name="to-save-a-project"></a>保存项目的步骤  
  
-   上**文件**菜单上，选择**保存**项目。  
  
如果项目中的数据库已更改，或尚未转换，SSMA 将提示你用于加载和保存元数据。 加载和保存元数据可以脱机工作。 它还允许你将完成的项目文件发送给其他人，（如技术支持人员）。 如果系统提示你保存元数据，请执行以下操作：  
  
1.  显示的状态的每个数据库**元数据缺少**，选择数据库名称旁边的复选框。 保存元数据可能需要几分钟。 如果您不想要在此时保存元数据，则不选择任何复选框。  
  
2.  单击 **“保存”**。  
  
SSMA 将分析 MySQL 架构并将元数据保存到项目文件。  
  
## <a name="opening-projects"></a>打开项目  
当你打开项目时，它已断开连接从 MySQL 和 SQL Server 或 SQL Azure。 这样可以脱机工作。 若要更新元数据，加载到 SQL Server 或 SQL Azure 数据库对象。 若要将数据迁移，你必须重新连接到 SQL Server 或 SQL Azure。  
  
##### <a name="to-open-a-project"></a>打开项目的步骤  
  
1.  可使用下列过程之一：  
  
    1.  上**文件**菜单上，指向**最近项目**。  
  
    2.  选择你想要打开的项目。  
  
    3.  上**文件**菜单上，选择**打开项目**，找到.m2ssproj 项目文件、 选择的文件，然后单击**打开**。  
  
2.  若要重新连接到 MySQL 上,**文件**菜单上，选择**重新连接到 MySQL**。  
  
3.  若要重新连接到 SQL Server 上**文件**菜单上，选择**重新连接到 SQL Server**。  
  
4.  若要重新连接到 SQL Azure 上**文件**菜单上，选择**重新连接到 SQL Azure。**  
  
## <a name="next-step"></a>下一步  
迁移过程的下一步是[连接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>另请参阅  
[连接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[迁移的 MySQL 数据库移到 SQL Server 的 Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[连接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[连接到 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
