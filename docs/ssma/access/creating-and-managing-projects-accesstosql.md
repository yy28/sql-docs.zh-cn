---
title: 创建和管理项目 (AccessToSQL) |Microsoft 文档
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
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
- creating projects
- new projects
- opening projects
- projects
- projects, creating and managing
- saving metadata
- saving projects
ms.assetid: f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 520d845124e2b176376bf6ece38e75e11bc58667
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="creating-and-managing-projects-accesstosql"></a>创建和管理项目 (AccessToSQL)
若要访问将数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，必须首先创建 SSMA 项目。 项目是一个文件，包含有关你想要迁移到 Access 数据库元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，元数据的目标实例的有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 迁移的对象和数据，将接收[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]连接信息和项目设置。  
  
## <a name="reviewing-default-project-settings"></a>查看默认项目设置  
SSMA 包含用于转换和同步数据库对象和数据进行相互转换的几个选项。 这些选项的默认设置是适用于多个用户。 但是，在创建新的 SSMA 项目之前，你应查看的选项，而且只要你愿意，更改将用于所有新项目的默认设置。  
  
**若要查看默认项目设置**  
  
1.  上**工具**菜单上，选择**默认项目设置**。  
  
2.  选择中的项目类型**迁移目标版本**下拉列表的设置是查看 / 更改，然后单击**常规**选项卡。  
  
3.  在左窗格中，单击**转换**。  
  
4.  在右窗格中，查看的选项。 有关这些选项的详细信息，请参阅[项目设置 （转换）](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)。  
  
5.  根据需要更改选项。  
  
6.  重复前面的步骤为**迁移**， **GUI**，和**类型映射**页。  
  
    -   有关迁移选项的信息，请参阅[项目设置 （迁移）](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d)。  
  
    -   有关用户界面选项的信息，请参阅[项目设置 (GUI)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
    -   有关数据类型映射设置的详细信息，请参阅[项目设置 （类型映射）](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655)。  
  
    -   有关 SQL Azure 设置信息，请参阅[项目设置 (SQL Azure)](http://msdn.microsoft.com/en-us/bbb8a204-d0e4-4f0b-9709-271feb1f136e)。  
  
**请注意**仅当你选择迁移到 SQL Azure 在创建项目时，可以使用 SQL Azure 设置。  
  
## <a name="creating-new-projects"></a>创建新项目  
无需加载默认项目启动 SSMA。 若要迁移到 Access 数据库中的数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，你必须创建一个项目。  
  
**若要创建新项目**  
  
1.  在“文件”菜单中，选择“新建项目”。  
  
    此时将显示“新建项目”  对话框。  
  
2.  在**名称**框中，输入你的项目的名称。  
  
3.  在**位置**框中，输入或选择用于项目的文件夹  
  
4.  在迁移到下拉朝下，选择一个 SQL Server 2005 / SQL Server 2008 / SQL Server 2012 / SQL Server 2014 / SQL Server 2016 / Azure SQL 数据库，然后单击**确定**。  
  
SSMA 创建项目文件。 现在，你可以执行的下一步[添加一个或多个访问数据库](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)。  
  
## <a name="customizing-project-settings"></a>自定义项目设置  
除了定义默认项目设置，将应用到所有新的 SSMA 项目，你还可以自定义的每个项目的设置。 有关详细信息，请参阅[设置转换和迁移选项](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167)。  
  
当你自定义源和目标数据库之间的数据类型映射时，你可以定义在项目、 数据库或对象级别的映射。 有关类型映射的信息的详细信息，请参阅[映射源和目标数据类型](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)。  
  
## <a name="saving-projects"></a>保存项目  
保存项目时，SSMA 仍然存在，项目设置中，和 （可选） 选择数据库元数据中的项目文件。  
  
**若要保存项目**  
  
-   上**文件**菜单上，选择**保存项目**。  
  
    如果项目中的数据库已更改，或尚未转换，SSMA 将提示你保存到项目的元数据。 保存元数据，可允许你脱机工作。 它还允许你将完成的项目文件发送给其他人，包括的技术支持人员。 如果系统提示你保存元数据，请执行以下操作：  
  
    1.  显示的状态的每个数据库**元数据缺少**，选择数据库名称旁边的复选框。  
  
        保存元数据可能需要几分钟。 如果您不想要在此时保存元数据，则不选择任何复选框。  
  
    2.  单击 **“保存”**。  
  
        SSMA 将分析访问架构，并将元数据保存到项目文件。  
  
## <a name="opening-projects"></a>打开项目  
当你打开的项目时，它从断开[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 这样可以脱机工作。 若要更新到对象的元数据加载数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 若要将数据迁移，必须重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
**若要打开的项目**  
  
1.  可使用下列过程之一：  
  
    -   上**文件**菜单上，指向**最近项目**，然后选择你想要打开的项目。  
  
    -   上**文件**菜单上，选择**打开项目**，找到.a2ssproj 项目文件、 选择的文件，然后单击**打开**。  
  
2.  若要重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]上**文件**菜单上，选择**重新连接到 SQL Server**。  
  
3.  若要重新连接到 SQL Azure 上**文件**菜单上，选择**重新连接到 SQL Azure。**  
  
## <a name="next-step"></a>下一步  
迁移过程的下一步是[添加一个或多个 Access 数据库](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)。  
  
## <a name="see-also"></a>另请参阅  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[添加和删除访问数据库文件](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)  
  
