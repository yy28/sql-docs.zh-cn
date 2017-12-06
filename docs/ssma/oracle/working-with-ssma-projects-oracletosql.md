---
title: "使用 SSMA 项目 (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Customizing Project Settings
ms.assetid: ee5d94c0-c7a6-4779-bd32-729bdaf61e1b
caps.latest.revision: "11"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.openlocfilehash: 3fbafb9a5357092aee293b9b190156d4bcca84d6
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="working-with-ssma-projects-oracletosql"></a>使用 SSMA 项目 (OracleToSQL)
若要迁移到的 Oracle 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，首先创建新的 SSMA 项目。 项目是一个文件，其中包含以下信息：  
  
-   你想要迁移到的 Oracle 数据库的相关元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   元数据的目标实例的有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中将接收迁移的对象和数据。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]连接信息。  
  
-   项目设置。  
  
当你打开的项目时，它断开 Oracle 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 允许您在脱机工作。 有关重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，请参阅[连接到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)。  
  
## <a name="reviewing-default-project-settings"></a>查看默认项目设置  
SSMA 进行转换和加载数据库对象，迁移数据，并且与 Oracle 同步 SSMA 包含多个设置和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 默认设置是适用于多个用户。 但是，在创建新的 SSMA 项目之前，你应查看这些设置。 如果你愿意，你可以更改将用于所有新项目的默认设置。  
  
**若要查看默认项目设置**  
  
1.  上**工具**菜单上，单击**默认项目设置**。  
  
2.  选择中的项目类型**迁移目标版本**下拉列表的设置所需查看或更改，然后单击**常规**选项卡。  
  
3.  在左窗格中，单击**转换**。  
  
4.  在右窗格中，查看并根据需要更改设置。 有关这些设置的详细信息，请参阅[项目设置 &#40;转换 &#41;&#40; OracleToSQL &#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
5.  重复步骤 1-3 的迁移、 同步、 加载系统对象、 GUI，和类型映射页。  
  
    -   有关迁移设置的信息，请参阅[项目设置 &#40;迁移 &#41;&#40; OracleToSQL &#41;](../../ssma/oracle/project-settings-migration-oracletosql.md).  
  
    -   有关系统对象设置的信息，请参阅[项目设置 &#40;加载系统对象 &#41;&#40; OracleToSQL &#41;](../../ssma/oracle/project-settings-loading-system-objects-oracletosql.md).  
  
    -   有关同步到的设置信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，请参阅[项目设置 &#40;同步 &#41;&#40; OracleToSQL &#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
    -   有关 GUI 设置的信息，请参阅[项目设置 &#40;GUI &#41;&#40; OracleToSQL &#41;](../../ssma/oracle/project-settings-gui-oracletosql.md).  
  
    -   有关数据类型映射设置的信息，请参阅[项目设置 &#40;类型映射 &#41;&#40; OracleToSQL &#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
## <a name="creating-new-projects"></a>创建新项目  
若要将数据从 Oracle 数据库到迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你必须首先创建一个项目。  
  
**创建项目**  
  
1.  上**文件**菜单上，单击**新项目**。  
  
    此时将显示“新建项目”  对话框。  
  
2.  在**名称**框中，输入你的项目的名称。  
  
3.  在**位置**框中，输入或选择用于该项目的文件夹，然后单击**确定**。  
  
4.  在**迁移到**下拉列表中，选择的目标版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]用于迁移。 可用选项包括：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016  
  
    -   Azure SQL 数据库  
  
## <a name="customizing-project-settings"></a>自定义项目设置  
除了定义应用于所有新的 SSMA 项目的默认项目设置，你可以自定义的每个项目的设置。 有关详细信息，请参阅[设置项目选项 &#40; OracleToSQL &#41;](../../ssma/oracle/setting-project-options-oracletosql.md)。  
  
当你自定义源和目标数据库之间的数据类型映射时，你可以定义在项目、 数据库或对象级别的映射。 有关详细信息，请参阅[映射 Oracle 和 SQL Server 数据类型 &#40; OracleToSQL &#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
## <a name="saving-projects"></a>保存项目  
保存项目时，SSMA 保留项目设置中，和 （可选） 选择数据库元数据中的项目文件。  
  
**若要保存项目**  
  
-   上**文件**菜单上，单击**保存项目**。  
  
    如果项目中的架构已更改，或尚未转换，SSMA 将提示你用于加载和保存元数据。 加载和保存元数据将让你脱机工作。 它还允许你将完成的项目文件发送给其他人，（如技术支持人员）。 如果系统提示你保存元数据，请执行以下操作：  
  
    1.  显示状态的每个架构**元数据缺少**，选择数据库名称旁边的复选框。  
  
        保存元数据可能需要几分钟。 如果你不想保存元数据，不选中所有复选框。  
  
    2.  单击**保存**按钮。  
  
        SSMA 将分析 Oracle 架构并将元数据保存到项目文件。  
  
## <a name="opening-projects"></a>打开项目  
当你打开项目时，它已断开连接从 Oracle 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 允许您在脱机工作。 若要更新元数据，数据库将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 若要将数据迁移，你必须重新连接到 Oracle 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
**若要打开的项目**  
  
1.  可使用下列过程之一：  
  
    -   上**文件**菜单上，指向**最近项目**，然后单击你想要打开的项目。  
  
    -   上**文件**菜单上，选择**打开项目**，找到.o2ssproj 项目文件、 选择的文件，然后单击**打开**。  
  
2.  在重新连接到 Oracle，**文件**菜单上，单击**重新连接到 Oracle**。  
  
3.  若要重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]上**文件**菜单上，单击**重新连接到 SQL Server**。  
  
## <a name="next-step"></a>下一步  
迁移过程的下一步是[连接到 Oracle 数据库 (OracleToSQL)](http://msdn.microsoft.com/en-us/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6)。  
  
## <a name="see-also"></a>另请参阅  
[将 Oracle 数据库迁移到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
[连接到 Oracle 数据库 &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)  
[连接到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
  
