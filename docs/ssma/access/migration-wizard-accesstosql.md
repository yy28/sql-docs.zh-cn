---
title: 迁移向导 (AccessToSQL) |Microsoft 文档
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
- Migration Wizard dialog box
- Migration Wizard, adding Access databases
- Migration Wizard, Connect to SQL Azure
- Migration Wizard, Connect to SQL Server
- Migration Wizard, Link Tables
- Migration Wizard, Migration status
- Migration Wizard, New Project
- Migration Wizard, Selecting objects to migrate
ms.assetid: 5bab5914-b2ae-4795-8cf5-83e42d64bef2
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 03b556d7fa5f49d69d9554d3416e3277adc4f504
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="migration-wizard-accesstosql"></a>迁移向导 (AccessToSQL)
迁移向导引导您完成迁移的一个或多个数据库从 Access 到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 通过使用向导，将创建一个项目，将数据库添加到项目，选择要迁移，并连接到的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 此外将转换、 加载和迁移访问架构和数据。 （可选） 你可以将链接到的访问表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 表。  
  
大多数迁移向导页面包含与现有的 SSMA 对话框相同的选项。 因此，下面将介绍向导的页面，以便你可以详细了解各个选项，然后提供链接。 如果某页包含唯一的选项，对它们进行此处记录。  
  
## <a name="starting-the-migration-wizard"></a>启动迁移向导  
默认情况下，迁移向导将显示当你启动 SSMA。 你还可以在启动向导**文件**通过选择菜单**迁移向导**。  
  
## <a name="welcome-page"></a>“欢迎”页  
欢迎页面介绍迁移向导，并提供以下选项启动向导。  
  
**启动时启动此向导。**  
默认情况下，SSMA 将开始迁移向导时启动 SSMA。 若要防止自动启动向导，请清除此复选框。  
  
## <a name="create-new-project-page"></a>创建新项目页  
创建新项目页中，你将输入的项目文件名称、 位置和迁移项目类型 （目标用于迁移的 SQL Server 的版本）。 有关详细信息，请参阅[新项目 (SSMA)](http://msdn.microsoft.com/en-us/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>添加访问数据库页  
添加 Access 数据库页是其中向项目中添加一个或多个访问数据库。 你可以通过单击添加单个数据库**添加数据库**，然后选择从数据库**打开**窗口。 或者，您可以通过使用发现数据库**查找数据库**按钮。 有关详细信息，请参阅以下主题：  
  
-   [添加和删除访问数据库文件](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)  
  
-   [查找数据库向导 （选择位置）](http://msdn.microsoft.com/en-us/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [查找数据库向导 （选择文件）](http://msdn.microsoft.com/en-us/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [查找数据库向导（验证所选内容）](http://msdn.microsoft.com/en-us/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>选择要迁移页面的对象  
在迁移页选择的对象，选择要转换的对象。 你可以选择的对象或单个对象的组的所有对象。  
  
**若要选择对象**  
  
1.  展开**访问元数据库**，然后展开**数据库**。  
  
2.  执行以下一项或多项操作：  
  
    -   若要转换的所有数据库，请旁边选中的复选框**数据库**。  
  
    -   若要将转换或省略单个数据库，选择或清除数据库名称旁边的复选框。  
  
    -   若要将转换或省略查询，展开数据库，然后选中或清除**查询**复选框。  
  
    -   若要将转换或省略各个表，展开数据库，展开**表**，然后选择或清除的表旁边的复选框。  
  
如果你有多个对象，你可能想要使用**高级对象选择**右窗格中的选项来筛选访问数据库对象。 例如，如果你选择**表**在左窗格中，然后可以通过输入字符串中的筛选的表的列表**筛选器**框。 然后可以选择或通过使用在窗格顶部的按钮清除迁移筛选的表。  
  
有关筛选的详细信息，请参阅选项部分的[（SSMA 常见） 的高级对象选择](http://msdn.microsoft.com/en-us/f53b0c79-5473-410a-a0dc-d8f544f7a63c)。  
  
## <a name="connect-to-sql-server-page"></a>连接到 SQL Server 页  
在连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]页上，指定连接属性，然后连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 有关详细信息，请参阅[连接到 SQL Server](http://msdn.microsoft.com/en-us/00e0432e-ec26-4ab4-af64-c9ca760e3541)  
  
> [!IMPORTANT]  
> 一旦连接成功，你将遇到**链接表**页面，其中有一个选项，链接表。 单击**下一步**并迁移开始。  
  
## <a name="connect-to-sql-azure-page"></a>连接到 SQL Azure 页  
在连接到 SQL Azure 页，你可以指定连接属性，然后连接到 SQL Azure。 若要创建新的 azure 数据库，则可以这样使用**创建 Azure 数据库**单击显示选项**浏览**按钮。 有关详细信息，请参阅[连接到 SQL Azure](http://msdn.microsoft.com/en-us/bf44b236-d9be-41ae-a5fd-bd73038e505f)  
  
> [!IMPORTANT]  
> 一旦连接成功，你将遇到**链接表**页面，其中有一个选项，链接表。 单击**下一步**按钮链接页后，可以开始迁移。  
  
## <a name="link-tables-page"></a>链接表页  
链接表页，可以将原始 Access 表链接到已迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 表。 链接表，以便你的查询、 窗体、 报表和数据访问页使用中的数据修改你的 Access 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库而不是你的 Access 数据库中的数据。  
  
**链接表**  
选择**链接表**复选框以 Access 表链接到已迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 表。 若要开始的迁移，则应单击**下一步**按钮。  
  
## <a name="migration-status-page"></a>迁移状态页  
迁移状态页显示的进度的转换访问架构写入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 架构，加载转换后的架构转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，然后迁移数据。  
  
有关此页的详细信息，请参阅[转换、 加载和迁移](http://msdn.microsoft.com/en-us/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>另请参阅  
[开始使用用于访问 SQL Server Migration Assistant &#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[用户界面 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
