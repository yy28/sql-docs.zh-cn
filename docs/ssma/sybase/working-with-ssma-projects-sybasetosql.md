---
title: 处理 SSMA 项目 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 11091d95-c488-48c3-891a-743cac94ac93
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7e1be086b891d6888c6509b15adc6664b3022978
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830125"
---
# <a name="working-with-ssma-projects-sybasetosql"></a>处理 SSMA 项目 (SybaseToSQL)
将 Sybase Adaptive Server Enterprise (ASE) 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，首先创建 SSMA 项目。 项目是一个包含你想要迁移到 ASE 数据库有关的元数据文件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，有关的目标实例的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 迁移的对象和数据，将接收[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure连接信息和项目设置。  
  
当您打开一个项目时，它从断开连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 这允许您脱机工作。 可以重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 有关详细信息，请参阅[连接到 SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [连接到 Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)。  
  
## <a name="reviewing-default-project-settings"></a>查看默认项目设置  
SSMA 包含多个选项进行转换和加载数据库对象，将迁移数据，并与 ASE 同步 SSMA 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 这些选项的默认设置是适用于多个用户。 但是，在创建新的 SSMA 项目之前，您应查看的选项和，如果需要，更改将用于所有新项目的默认值。  
  
**若要查看默认项目设置**  
  
1.  上**工具**菜单中，选择**默认项目设置**。  
  
2.  选择项目类型中的**迁移目标版本**下拉列表中的哪些是需要设置要查看或更改，然后单击**常规**选项卡。  
  
3.  在左窗格中，单击**转换**。  
  
4.  在右窗格中，查看选项，可根据需要更改。 有关这些选项的详细信息，请参阅[项目设置&#40;转换&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)。  
  
5.  重复步骤 1-3 的迁移、 SQL Azure、 正在加载对象、 GUI，和类型映射页。  
  
    -   有关迁移选项的信息，请参阅[项目设置&#40;迁移&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)。  
  
    -   加载到对象的选项有关的信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[项目设置&#40;同步&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)。  
  
    -   有关 GUI 选项的详细信息，请参阅[项目设置&#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)。  
  
    -   有关数据类型映射设置的详细信息，请单击[项目设置&#40;类型映射&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)。  
  
    -   有关 SQL Azure 选项的详细信息，请参阅[项目设置&#40;Azure SQL DB &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)。  
  
    > [!NOTE]  
    > 只能在选择时，将显示 SQL Azure 设置**迁移到 SQL Azure**创建项目时。  
  
## <a name="creating-new-projects"></a>创建新项目  
若要将数据从 ASE 数据库迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，必须首先创建一个项目。  
  
**若要创建项目**  
  
1.  在“文件”菜单中，选择“新建项目”。  
  
    此时将显示“新建项目”  对话框。  
  
2.  在中**名称**框中，输入你的项目的名称。  
  
3.  在中**位置**框中，输入或选择该项目的文件夹。  
  
4.  在中**迁移到**下拉列表中，选择的目标版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用于迁移。 可用选项包括：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL DB  
  
然后单击**确定**。  
  
## <a name="customizing-project-settings"></a>自定义项目设置  
除了定义应用于所有新的 SSMA 项目的默认项目设置，可以自定义每个项目的设置。 有关详细信息，请参阅[设置项目选项&#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)。  
  
自定义源和目标数据库之间的数据类型映射时，可以定义项目、 数据库或对象级别上的映射。 有关类型映射的详细信息，请参阅[映射 Sybase ASE 和 SQL Server 数据类型&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
## <a name="saving-projects"></a>正在保存项目  
当保存项目时，SSMA 将保留项目设置，和 （可选） 数据库元数据，对项目文件。  
  
**若要保存项目**  
  
-   上**文件**菜单中，选择**保存项目**。  
  
    如果在项目中的数据库已更改，或者尚未转换，SSMA 将提示您保存到项目的元数据。 保存元数据将允许您脱机工作，并将完整的项目文件发送给其他人，包括技术支持人员。 如果系统提示保存元数据，请执行以下操作：  
  
    1.  为每个数据库的状态显示**元数据缺少**，选择数据库名称旁边的复选框。  
  
        正在保存元数据可能需要几分钟的时间。 如果您不想要现在保存元数据，则选择任何复选框。  
  
    2.  单击**保存**按钮。  
  
        SSMA 将 Sybase ASE 架构中分析并将元数据保存到项目文件。  
  
## <a name="opening-projects"></a>打开项目  
从 ASE 和断开时打开的项目，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 这允许您脱机工作。 若要更新的元数据，数据库将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 若要将数据迁移，必须重新连接到 ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
**若要打开的项目**  
  
1.  可使用下列过程之一：  
  
    -   上**文件**菜单，依次指向**最近使用的项目**，然后选择你想要打开的项目。  
  
    -   上**文件**菜单中，选择**打开项目**，找到.s2ssproj 项目文件中，选择的文件，然后单击**打开**。  
  
2.  若要重新连接到 ASE 中，在**文件**菜单中，选择**重新连接到 Sybase**。  
  
3.  若要重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 上**文件**菜单中，选择**重新连接到 SQL Server** / **重新连接到 SQL Azure**。  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是[连接到 Sybase ASE](connecting-to-sybase-ase-sybasetosql.md)。  
  
## <a name="see-also"></a>请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[连接到 Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[连接到 SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[连接到 Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
