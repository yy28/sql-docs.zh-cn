---
title: 处理 SSMA 项目 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 07abef8a-28e8-4a66-927c-c9a5b8c938ef
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: bb43fabb2592b6d82d3fb6d14f516bfdd0029bdc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47775097"
---
# <a name="working-with-ssma-projects-db2tosql"></a>处理 SSMA 项目 (DB2ToSQL)
将 DB2 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，首先创建 SSMA 项目。 项目是一个文件包含以下信息：  
  
-   有关你想要迁移到 DB2 数据库的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   有关的目标实例的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将接收迁移的对象和数据。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接信息。  
  
-   项目设置。  
  
当您打开一个项目时，它从 DB2 断开连接和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 允许您在脱机工作。 了解如何重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[连接到 SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)。  
  
## <a name="reviewing-default-project-settings"></a>查看默认项目设置  
SSMA 进行转换和加载数据库对象、 迁移数据，和与 DB2 同步 SSMA 包含多个设置和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 默认设置是适用于多个用户。 但是，创建一个新的 SSMA 项目之前，应查看的设置。 如果愿意，可以更改将用于所有新项目的默认设置。  
  
**若要查看默认项目设置**  
  
1.  上**工具**菜单上，单击**默认项目设置**。  
  
2.  选择项目类型中的**迁移目标版本**下拉列表中的哪些是需要设置要查看或更改，然后单击**常规**选项卡。  
  
3.  在左窗格中，单击**转换**。  
  
4.  在右窗格中，查看并根据需要更改的设置。 有关这些设置的详细信息，请参阅[项目设置&#40;转换&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)。  
  
5.  重复步骤 1-3 的迁移、 同步、 加载系统对象、 GUI，和类型映射页。  
  
    -   有关迁移设置的信息，请参阅[项目设置&#40;迁移&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-migration-db2tosql.md)。  
  
    -   有关系统对象设置的信息，请参阅[项目设置&#40;加载系统对象&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-loading-system-objects-db2tosql.md)。  
  
    -   有关设置同步到信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[项目设置&#40;同步&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)。  
  
    -   有关 GUI 设置的信息，请参阅[项目设置&#40;GUI&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-gui-db2tosql.md)。  
  
    -   有关数据类型映射设置的信息，请参阅[项目设置&#40;类型映射&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)。  
  
## <a name="creating-new-projects"></a>创建新项目  
若要将数据从 DB2 数据库到迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，首先必须创建一个项目。  
  
**若要创建项目**  
  
1.  上**文件**菜单上，单击**新项目**。  
  
    此时将显示“新建项目”  对话框。  
  
2.  在中**名称**框中，输入你的项目的名称。  
  
3.  在中**位置**框中，输入或选择的项目文件夹，然后单击**确定**。  
  
4.  在中**迁移到**下拉列表中，选择的目标版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用于迁移。 可用选项包括：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL DB  
  
## <a name="customizing-project-settings"></a>自定义项目设置  
除了定义应用于所有新的 SSMA 项目的默认项目设置，可以自定义每个项目的设置。 有关详细信息，请参阅[设置项目选项&#40;OracleToSQL&#41; ](../../ssma/oracle/setting-project-options-oracletosql.md)和相关的部分。  
  
自定义源和目标数据库之间的数据类型映射时，可以定义项目、 数据库或对象级别上的映射。 有关详细信息，请参阅[映射 DB2 和 SQL Server 数据类型&#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)。  
  
## <a name="saving-projects"></a>正在保存项目  
当保存项目时，SSMA 将保留项目设置，和 （可选） 数据库元数据，对项目文件。  
  
**若要保存项目**  
  
-   上**文件**菜单上，单击**保存项目**。  
  
    如果项目中的架构已更改，或者尚未转换，SSMA 将提示您加载和保存元数据。 加载和保存元数据将允许您脱机工作。 它还允许您将完整的项目文件发送给其他人，例如技术支持人员。 如果系统提示保存元数据，请执行以下操作：  
  
    1.  有关显示的状态为每个架构**元数据缺少**，选择数据库名称旁边的复选框。  
  
        正在保存元数据可能需要几分钟的时间。 如果您不希望保存元数据，不选中任何复选框。  
  
    2.  单击**保存**按钮。  
  
        SSMA 会分析 DB2 架构并将元数据保存到项目文件。  
  
## <a name="opening-projects"></a>打开项目  
从 DB2 和断开时打开的项目， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 允许您在脱机工作。 若要更新的元数据，数据库将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 若要将数据迁移，必须重新连接到 DB2 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
**若要打开的项目**  
  
1.  可使用下列过程之一：  
  
    -   上**文件**菜单，依次指向**最近使用的项目**，然后单击你想要打开的项目。  
  
    -   上**文件**菜单中，选择**打开项目**，找到.o2ssproj 项目文件中，选择的文件，然后单击**打开**。  
  
2.  若要重新连接到 DB2，在**文件**菜单上，单击**重新连接到 DB2**。  
  
3.  若要重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然后在**文件**菜单中，单击**重新连接到 SQL Server**。  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是[连接到 DB2 数据库](http://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844)。  
  
## <a name="see-also"></a>请参阅  
[迁移的 DB2 数据库移到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
[连接到 DB2 数据库&#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
[连接到 SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
  
