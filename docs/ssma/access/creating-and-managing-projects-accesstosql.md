---
title: 创建和管理项目 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- creating projects
- new projects
- opening projects
- projects
- projects, creating and managing
- saving metadata
- saving projects
ms.assetid: f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: abbe0746193df3fe341b4f66086291dc1055e11b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006617"
---
# <a name="creating-and-managing-projects-accesstosql"></a>创建和管理项目 (AccessToSQL)
将 Access 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，必须首先创建 SSMA 项目。 项目是一个包含有关你想要迁移到 Access 数据库的元数据文件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，有关的目标实例的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 迁移的对象和数据，将接收[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]连接信息和项目设置。  
  
## <a name="reviewing-default-project-settings"></a>查看默认项目设置  
SSMA 包含多个选项用于将转换和同步数据库对象，并将数据转换。 这些选项的默认设置是适用于多个用户。 但是，在创建新的 SSMA 项目之前，您应查看的选项和，如果需要，更改将用于所有新项目的默认设置。  
  
**若要查看默认项目设置**  
  
1.  上**工具**菜单中，选择**默认项目设置**。  
  
2.  选择项目类型中的**迁移目标版本**哪些设置需要查看 / 更改和然后单击下拉列表**常规**选项卡。  
  
3.  在左窗格中，单击**转换**。  
  
4.  在右窗格中查看的选项。 有关这些选项的详细信息，请参阅[项目设置 （转换）](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)。  
  
5.  根据需要更改选项。  
  
6.  重复前面的步骤对于**迁移**， **GUI**，并**类型映射**页。  
  
    -   有关迁移选项的信息，请参阅[项目设置 （迁移）](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)。  
  
    -   有关用户界面选项的信息，请参阅[项目设置 (GUI)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
    -   有关数据类型映射设置的详细信息，请参阅[项目设置 （类型映射）](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)。  
  
    -   有关 SQL Azure 设置信息，请参阅[项目设置 (SQL Azure)](https://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)。  
  
**请注意**仅当选择迁移到 SQL Azure 在创建项目时，可以使用 SQL Azure 设置。  
  
## <a name="creating-new-projects"></a>创建新项目  
SSMA 启动而不加载默认项目。 若要将数据从到 Access 数据库迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，必须创建一个项目。  
  
**若要创建新项目**  
  
1.  在“文件”菜单中，选择“新建项目”。    
  
    此时将显示“新建项目”  对话框。  
  
2.  在中**名称**框中，输入你的项目的名称。  
  
3.  在中**位置**框中，输入或选择该项目的文件夹  
  
4.  在迁移到下拉菜单中，选择一个 SQL Server 2005 / SQL Server 2008 / SQL Server 2012 / SQL Server 2014 / SQL Server 2016 / Azure SQL 数据库，然后单击**确定**。  
  
SSMA 会创建项目文件。 现在可以执行的下一步[添加一个或多个 Access 数据库](adding-and-removing-access-database-files-accesstosql.md)。  
  
## <a name="customizing-project-settings"></a>自定义项目设置  
除了定义默认项目设置，将应用到所有新的 SSMA 项目，你还可以定义每个项目的设置。 有关详细信息，请参阅[设置转换和迁移选项](setting-conversion-and-migration-options-accesstosql.md)。  
  
自定义源和目标数据库之间的数据类型映射时，可以定义项目、 数据库或对象级别上的映射。 有关类型映射的详细信息，请参阅[映射源和目标数据类型](mapping-source-and-target-data-types-accesstosql.md)。  
  
## <a name="saving-projects"></a>正在保存项目  
当您保存项目时，SSMA 仍然存在，项目设置，和 （可选） 数据库元数据，对项目文件。  
  
**若要保存项目**  
  
-   上**文件**菜单中，选择**保存项目**。  
  
    如果在项目中的数据库已更改，或者尚未转换，SSMA 将提示您保存到项目的元数据。 保存元数据，可脱机工作。 它还允许您将完整的项目文件发送给其他人，包括技术支持人员。 如果系统提示保存元数据，请执行以下操作：  
  
    1.  为每个数据库的状态显示**元数据缺少**，选择数据库名称旁边的复选框。  
  
        正在保存元数据可能需要几分钟的时间。 如果您不想要现在保存元数据，则选择任何复选框。  
  
    2.  单击“保存”  。  
  
        SSMA 会分析访问架构，并将元数据保存到项目文件。  
  
## <a name="opening-projects"></a>打开项目  
当您打开一个项目时，它从断开连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 这允许您脱机工作。 若要更新的元数据加载到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 若要将数据迁移，必须重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
**若要打开的项目**  
  
1.  可使用下列过程之一：  
  
    -   上**文件**菜单，依次指向**最近使用的项目**，然后选择你想要打开的项目。  
  
    -   上**文件**菜单中，选择**打开项目**，找到.a2ssproj 项目文件中，选择的文件，然后单击**打开**。  
  
2.  若要重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然后在**文件**菜单中，选择**重新连接到 SQL Server**。  
  
3.  若要重新连接到 SQL Azure 上**文件**菜单中，选择**重新连接到 SQL Azure。**  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是[添加一个或多个 Access 数据库](adding-and-removing-access-database-files-accesstosql.md)。  
  
## <a name="see-also"></a>请参阅  
[Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[添加和删除访问数据库文件](adding-and-removing-access-database-files-accesstosql.md)  
  
