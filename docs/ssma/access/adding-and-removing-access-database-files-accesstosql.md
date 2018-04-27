---
title: 添加和删除访问数据库文件 (AccessToSQL) |Microsoft 文档
ms.prod: sql
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
- Access databases
- adding Access files
- adding and removing Access databases
- browsing Access metadata
- browsing metadata, Access databases
- connecting, Access databases
- databases
- files, adding and removing
- finding Access databases
- finding database files
- locating database files
- metadata
- metadata, browsing
- metadata, refreshing
- refreshing metadata
- removing Access files
- scanning for database files
- searching for database files
ms.assetid: e944c740-4c8a-4bc1-b0ed-be57bc06dced
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc44607d172ebc1f8d7d09b68ba77d68002de2bb
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>添加和删除访问数据库文件 (AccessToSQL)
若要迁移 Access 数据移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，必须将一个或多个访问数据库添加到 SSMA 项目。 这些数据库必须 Access 97 或更高版本。 如果你的数据库从早期版本的访问，你必须将数据库转换为较新版本。 通过打开并将数据库保存 Access 97 或更高版本中，添加到 SSMA 之前执行此操作。  
  
## <a name="what-happens-when-you-add-access-database-files"></a>添加 Access 数据库文件时，会发生什么情况？  
当你将 Access 数据库添加到的 SSMA 项目时，SSMA 读取数据库元数据，然后将此元数据添加到项目文件。 此元数据描述数据库和它的对象。 SSMA 使用的元数据转换到的对象时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 语法时，它将迁移到的数据和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 你可以浏览此访问元数据资源管理器中的元数据，并检查各个数据库对象的属性。  
  
> [!NOTE]  
> Access 数据库可以拆分为多个文件： 包含表的后端数据库和包含查询、 窗体、 报表、 宏、 模块和快捷方式的前端数据库。 如果你想要拆分将数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，将前端数据库添加到 SSMA。  
  
## <a name="permissions-that-are-required-by-ssma"></a>所需的 SSMA 的权限  
若要迁移到 Access 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure、 用户组和管理员用户必须具有管理权限。 有关如何迁移使用工作组保护的数据库的信息，请参阅[准备迁移的 Access 数据库](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
## <a name="selecting-databases-to-add"></a>选择要添加的数据库  
如果你想要将一个或多个数据库添加到 SSMA 项目，并且文件都在一个已知位置，你可以通过使用以下过程来添加文件。  
  
**若要添加单个数据库文件**  
  
1.  上**文件**菜单上，单击**添加数据库**。  
  
2.  在**打开**对话框框中，找到包含的数据库文件的文件夹。  
  
3.  选择你想要添加，，然后单击的文件**打开**。  
  
## <a name="finding-databases-to-add"></a>查找要添加的数据库  
如果你想要从不同的文件夹的访问的多个数据库添加到 SSMA 项目，或者你想要添加单个文件，但是找不到文件，你可以按照这些步骤，若要查找更多的文件之一并将它们添加到项目。  
  
**可以查找和添加数据库**  
  
1.  上**文件**菜单上，单击**查找数据库**。  
  
2.  在查找数据库向导中，输入驱动器、 文件路径或你想要搜索的 UNC 路径的名称。 或者，单击**浏览**以找到驱动器或网络文件夹。  
  
3.  单击**添加**将位置添加到列表。  
  
    重复前面的两个步骤以添加更多搜索位置。  
  
4.  （可选） 添加搜索条件来完善的返回的数据库列表。  
  
    > [!IMPORTANT]  
    > **文件名称的全部或部分**文本框中不支持通配符。  
  
5.  单击**扫描**。  
  
    将显示扫描页。 这将显示已发现的数据库和搜索的进度。 若要停止搜索，请单击**停止**。  
  
6.  在选择文件页上，选择你想要添加到项目的数据库。  
  
    你可以使用**选择所有**和**清除所有**要选中或清除所有数据库的列表顶部的按钮。 你可以按住 CTRL 键来选择多个数据库，或按住 SHIFT 键以选择一系列数据库。  
  
7.  单击“下一步” 。  
  
8.  在验证页上，单击**完成**。  
  
## <a name="browsing-access-metadata"></a>浏览访问元数据  
Access 数据库添加到项目后，在访问元数据资源管理器将显示项目元数据。 您可以浏览数据库和资源管理器中的数据库对象的层次结构。  
  
**若要浏览元数据**  
  
1.  在访问元数据资源管理器中，展开**访问元数据库**，然后展开**数据库**。  
  
2.  展开你想要查看，然后展开数据库**查询**。  
  
    请注意查询的列表。 如果你选择查询， **SQL**选项卡和**属性**选项卡会显示在右窗格中。  
  
3.  展开**表**，然后选择一个表。  
  
    请注意，四个选项卡显示：**表**，**类型映射**，**属性**，和**数据**。  
  
4.  展开表，再展开**密钥**，然后选择一个密钥。  
  
    在右窗格中显示的键属性。  
  
5.  展开**索引**，然后选择索引。  
  
    索引属性显示在右窗格中。  
  
## <a name="refreshing-databases"></a>刷新数据库  
如果访问数据库更改将添加其文件后，你可以更新元数据从访问数据库。  
  
**若要更新访问元数据**  
  
-   在访问元数据资源管理器中，右键单击数据库，，然后选择**从数据库刷新**。  
  
## <a name="removing-databases"></a>删除数据库  
你可以通过执行以下步骤从项目中移除的 Access 数据库。  
  
**从项目中删除数据库**  
  
1.  在访问元数据资源管理器中，展开**访问元数据库**，然后展开**数据库**。  
  
2.  右键单击数据库，，然后选择**删除数据库**。  
  
## <a name="next-step"></a>下一步  
迁移过程的下一步是[连接到 SQL Server](http://msdn.microsoft.com/en-us/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)。  
  
## <a name="see-also"></a>另请参阅  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[创建和管理项目](http://msdn.microsoft.com/en-us/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7)  
  
