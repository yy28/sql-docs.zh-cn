---
title: 处理 SSMA 项目 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 518f899118d5a7d2dce4f56d185fce9d5b1e47df
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661666"
---
# <a name="working-with-ssma-projects-mysqltosql"></a>处理 SSMA 项目 (MySQLToSQL)
若要将 MySQL 数据库迁移到 SQL Server 或 SQL Azure，必须首先创建 SSMA 项目。 项目是一个文件包含以下信息：  
  
-   你想要迁移到 SQL Server 或 SQL Azure 的 MySQL 数据库的相关元数据。  
  
-   有关 SQL Server 或 SQL Azure 迁移的对象和数据将接收的目标实例的元数据。  
  
-   SQL Server 或 SQL Azure 连接信息。  
  
-   项目设置。  
  
当您打开一个项目时，它是从 MySQL 和 SQL Server 或 SQL Azure 断开连接。 允许您在脱机工作。 重新连接到 SQL Server 的详细信息，请参阅[连接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="reviewing-default-project-settings"></a>查看默认项目设置  
SSMA 进行转换和加载数据库、 迁移数据，和与 MySQL 和 SQL Server 或 SQL Azure 同步 SSMA 包含多个设置。 默认设置是适用于多个用户。 但是，创建一个新的 SSMA 项目之前，应查看的设置。 如果需要，可以更改将用于所有新项目的默认设置。  
  
##### <a name="to-review-default-project-settings"></a>若要查看默认项目设置  
  
1.  选择**默认项目设置**从**工具**菜单。  
  
2.  选择项目类型中的**迁移目标版本**哪些设置需要查看 / 更改和然后单击下拉列表**常规**选项卡。  
  
3.  在左窗格中，单击**转换**。  
  
4.  在右窗格中，查看并根据需要更改的设置。 有关这些设置的详细信息，请参阅[项目设置&#40;转换&#41; &#40;MySQLToSQL&#41; ](../../ssma/mysql/project-settings-conversion-mysqltosql.md) 。  
  
5.  重复步骤 1-3 的迁移、 同步、 SQL Azure、 GUI，和类型映射页。  
  
-   有关迁移设置的信息，请参阅[项目设置&#40;迁移&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)。  
  
-   有关 SQL Server 的同步设置的信息，请参阅[项目设置&#40;同步&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)。  
  
-   有关 GUI 设置的信息，请参阅[项目设置 (GUI) （SSMA 常见）](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
-   有关数据类型映射设置的信息，请参阅[项目设置&#40;类型映射&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)。  
  
-   有关 SQL Azure 设置信息，请参阅[项目设置&#40;Azure SQL DB&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)。  
  
> [!NOTE]  
> 只能在选择时，将显示 SQL Azure 设置**迁移到 SQL Azure**创建项目时。  
  
## <a name="creating-new-projects"></a>创建新项目  
若要将数据从 MySQL 数据库迁移到 SQL Server 或 SQL Azure，必须创建一个项目。  
  
##### <a name="to-create-a-new-project"></a>创建新项目的步骤  
  
1.  选择**新的项目**从**文件**菜单。 此时将显示“新建项目”  对话框。 在“文件”菜单中，选择“新建项目”。 此时将显示“新建项目”  对话框。  
  
2.  在中**名称**框中，输入你的项目的名称。  
  
3.  在中**位置**框中，输入或选择该项目的文件夹。  
  
4.  在中**迁移到**下拉列表中，选择的目标版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用于迁移。 可用选项包括：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   Azure SQL DB  
  
然后单击**确定**  
  
SSMA 会创建项目文件。  
  
## <a name="customizing-project-settings"></a>自定义项目设置  
除了定义默认值应用于所有新的 SSMA 项目的项目设置还可以定制为每个项目的设置。 有关详细信息，请参阅[设置项目选项&#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)。  
  
自定义源和目标数据库之间的数据类型映射时，可以定义项目、 数据库或对象级别上的映射。 有关详细信息，请参阅[映射 MySQL 和 SQL Server 数据类型&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)。  
  
## <a name="saving-projects"></a>正在保存项目  
保存项目功能允许用户实质上是将项目设置和数据库元数据 （可选） 保存到 SSMA 项目文件。  
  
##### <a name="to-save-a-project"></a>保存项目的步骤  
  
-   上**文件**菜单中，选择**保存**项目。  
  
如果在项目中的数据库已更改，或者尚未转换，SSMA 将提示您加载和保存元数据。 加载和保存元数据可脱机工作。 它还允许您将完整的项目文件发送给其他人，例如技术支持人员。 如果系统提示保存元数据，请执行以下操作：  
  
1.  为每个数据库的状态显示**元数据缺少**，选择数据库名称旁边的复选框。 正在保存元数据可能需要几分钟的时间。 如果您不想要现在保存元数据，则选择任何复选框。  
  
2.  单击 **“保存”**。  
  
SSMA 将 MySQL 架构中分析并将元数据保存到项目文件。  
  
## <a name="opening-projects"></a>打开项目  
当您打开一个项目时，请断开从 MySQL 和 SQL Server 或 SQL Azure。 这允许您脱机工作。 若要更新元数据，加载到 SQL Server 或 SQL Azure 数据库对象。 若要将数据迁移，你必须重新连接到 SQL Server 或 SQL Azure。  
  
##### <a name="to-open-a-project"></a>打开项目的步骤  
  
1.  可使用下列过程之一：  
  
    1.  上**文件**菜单，依次指向**最近使用的项目**。  
  
    2.  选择你想要打开的项目。  
  
    3.  上**文件**菜单中，选择**打开项目**，找到.m2ssproj 项目文件中，选择的文件，然后单击**打开**。  
  
2.  若要重新连接到 MySQL 上,**文件**菜单中，选择**重新连接到 MySQL**。  
  
3.  若要重新连接到 SQL Server 上**文件**菜单中，选择**重新连接到 SQL Server**。  
  
4.  若要重新连接到 SQL Azure 上**文件**菜单中，选择**重新连接到 SQL Azure。**  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是[连接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>请参阅  
[连接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[迁移 MySQL 数据库移到 SQL Server-Azure SQL 数据库&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[连接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[连接到 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
