---
title: 迁移向导 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration Wizard dialog box
- Migration Wizard, adding Access databases
- Migration Wizard, Connect to SQL Azure
- Migration Wizard, Connect to SQL Server
- Migration Wizard, Link Tables
- Migration Wizard, Migration status
- Migration Wizard, New Project
- Migration Wizard, Selecting objects to migrate
ms.assetid: 5bab5914-b2ae-4795-8cf5-83e42d64bef2
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0c77ff9dae7d6d700289cdff4daff56ba4457651
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636195"
---
# <a name="migration-wizard-accesstosql"></a>迁移向导 (AccessToSQL)
迁移向导将引导您完成的一个或多个数据库迁移从 Access 到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 通过使用该向导，将创建一个项目，将数据库添加到项目，选择要迁移，并连接到对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 此外将转换、 加载和迁移 Access 架构和数据。 （可选） 可以链接到访问表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表。  
  
大多数迁移向导页包含与现有的 SSMA 对话框相同的选项。 因此，本文所述的向导页，然后提供链接，以便您可以详细了解各个选项。 如果页面包含唯一的选项，它们将加以介绍。  
  
## <a name="starting-the-migration-wizard"></a>启动迁移向导  
默认情况下，迁移向导启动 SSMA 时出现。 此外可以在启动向导**文件**菜单中的选择**迁移向导**。  
  
## <a name="welcome-page"></a>“欢迎”页  
欢迎页面介绍迁移向导，并提供以下选项用于启动该向导。  
  
**启动时启动此向导。**  
默认情况下，SSMA 将启动迁移向导启动 SSMA。 若要防止自动启动该向导，请清除此复选框。  
  
## <a name="create-new-project-page"></a>创建新的项目页  
创建新项目页是你在其中输入项目文件名称、 位置和迁移项目类型 （目标用于迁移 SQL Server 的版本）。 有关详细信息，请参阅[新项目 (SSMA)](http://msdn.microsoft.com/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>添加访问数据库页  
添加 Access 数据库页是在其中将一个或多个 Access 数据库添加到项目。 您可以通过单击添加单独的数据库**添加数据库**，然后选择从数据库**打开**窗口。 或者，你可以通过使用查找数据库**查找数据库**按钮。 有关详细信息，请参阅以下主题：  
  
-   [添加和删除访问数据库文件](adding-and-removing-access-database-files-accesstosql.md)  
  
-   [查找数据库向导 （选择位置）](http://msdn.microsoft.com/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [查找数据库向导 （选择文件）](http://msdn.microsoft.com/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [查找数据库向导（验证所选内容）](http://msdn.microsoft.com/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>选择要迁移页对象  
在迁移页面上选择的对象，可选择要转换的对象。 可以选择的对象或单个对象的组的所有对象。  
  
**若要选择的对象**  
  
1.  展开**访问元数据库**，然后展开**数据库**。  
  
2.  执行以下一项或多项操作：  
  
    -   若要将所有数据库，选择复选框旁边**数据库**。  
  
    -   若要将转换或省略单独的数据库，选择或清除的数据库名称旁边的复选框。  
  
    -   若要将转换或省略查询，再展开数据库，然后选中或清除**查询**复选框。  
  
    -   若要将转换或忽略各个表，展开数据库，展开**表**，然后选中或清除表旁边的复选框。  
  
如果有多个对象，您可能想要使用**高级对象选择**右窗格中的选项来筛选访问数据库对象。 例如，如果您选择**表**在左窗格中，然后可以通过输入中的字符串筛选的表列表**筛选器**框。 您然后可以选择或清除已筛选的表迁移为使用窗格顶部的按钮。  
  
有关筛选的详细信息，请参阅的选项部分[（SSMA 常见） 的高级对象选择](http://msdn.microsoft.com/f53b0c79-5473-410a-a0dc-d8f544f7a63c)。  
  
## <a name="connect-to-sql-server-page"></a>连接到 SQL Server 页  
在连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]页上，指定连接属性，然后连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[连接到 SQL Server](http://msdn.microsoft.com/00e0432e-ec26-4ab4-af64-c9ca760e3541)  
  
> [!IMPORTANT]  
> 一旦连接成功，将会遇到**链接表**页面，其中有一个链接表的选项。 单击**下一步**并启动迁移。  
  
## <a name="connect-to-sql-azure-page"></a>连接到 SQL Azure 的页  
在连接到 SQL Azure 页上，您指定连接属性，然后连接到 SQL Azure。 若要创建新的 azure 数据库，可以执行使用这样**创建 Azure 数据库**的单击显示的选项**浏览**按钮。 有关详细信息，请参阅[连接到 SQL Azure](connect-to-azure-sql-db-accesstosql.md)  
  
> [!IMPORTANT]  
> 一旦连接成功，将会遇到**链接表**页面，其中有一个链接表的选项。 单击**下一步**按钮上的链接页后，可以开始迁移。  
  
## <a name="link-tables-page"></a>链接表页  
链接表页，可以将原始 Access 表链接到已迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表。 链接表，以便你的查询、 窗体、 报表和数据访问页使用中的数据修改你的 Access 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 数据库而不是你的 Access 数据库中的数据。  
  
**链接表**  
选择**链接表**复选框以 Access 表链接到已迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表。 若要开始的迁移，则应单击**下一步**按钮。  
  
## <a name="migration-status-page"></a>迁移状态页  
迁移状态页会显示将转换为 Access 架构的进度[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 架构加载到转换后的架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，然后将迁移数据。  
  
有关此页的详细信息，请参阅[转换、 加载和迁移](http://msdn.microsoft.com/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>请参阅  
[开始使用用于访问 SQL Server 迁移助手&#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[用户界面 Reference(Access)](http://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
