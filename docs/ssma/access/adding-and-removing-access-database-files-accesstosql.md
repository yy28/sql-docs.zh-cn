---
title: 添加和删除访问数据库文件 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8de9b27a58d277191a4d40da6b34dbcbbd43e497
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51655636"
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>添加和删除访问数据库文件 (AccessToSQL)
若要访问将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，必须将一个或多个 Access 数据库添加到 SSMA 项目。 这些数据库必须是 Access 97 或更高版本。 如果是从早期版本的访问权限的数据库，必须将数据库转换到较新版本。 通过打开和保存数据库 Access 97 或更高版本中，添加到 SSMA 之前执行此操作。  
  
## <a name="what-happens-when-you-add-access-database-files"></a>添加 Access 数据库文件时，会发生什么情况？  
当将 Access 数据库添加到 SSMA 项目时，SSMA 读取数据库元数据，然后将此元数据添加到项目文件。 此元数据描述的数据库和它的对象。 SSMA 将转换到的对象时使用的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 语法时，它将迁移到的数据和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 您可以浏览访问元数据资源管理器中的此元数据，并查看单独的数据库对象的属性。  
  
> [!NOTE]  
> Access 数据库可以拆分为多个文件： 包含表，一个后端数据库和包含查询、 窗体、 报表、 宏、 模块和快捷方式的前端数据库。 如果你想要拆分数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，将前端数据库添加到 SSMA。  
  
## <a name="permissions-that-are-required-by-ssma"></a>权限所需的 SSMA  
若要迁移到 Access 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure、 用户组和管理员用户必须具有管理权限。 有关如何迁移具有工作组保护的数据库的信息，请参阅[迁移准备 Access 数据库](preparing-access-databases-for-migration-accesstosql.md)。  
  
## <a name="selecting-databases-to-add"></a>选择要添加的数据库  
如果你想要将一个或多个数据库添加到一个 SSMA 项目，并且这些文件并全部放在一个已知位置，可以通过使用以下过程来添加文件。  
  
**若要添加单独的数据库文件**  
  
1.  上**文件**菜单上，单击**添加数据库**。  
  
2.  在中**打开**对话框框中，找到包含的数据库文件的文件夹。  
  
3.  选择你想要添加，并单击的文件**打开**。  
  
## <a name="finding-databases-to-add"></a>查找要添加的数据库  
如果你想要将多个访问数据库从不同的文件夹添加到一个 SSMA 项目，或者想要添加单个文件，但是若要查找该文件，可以按照以下步骤来找到更多的文件之一并将其添加到项目。  
  
**若要查找和添加数据库**  
  
1.  上**文件**菜单上，单击**查找数据库**。  
  
2.  在查找数据库向导中，输入驱动器、 文件路径或想要搜索的 UNC 路径的名称。 或者，单击**浏览**以找到驱动器或网络文件夹。  
  
3.  单击**添加**将位置添加到列表。  
  
    重复前面的两个步骤以添加更多的搜索位置。  
  
4.  （可选） 添加搜索条件来完善的数据库返回的列表。  
  
    > [!IMPORTANT]  
    > **全部或部分文件名**文本框中不支持通配符字符。  
  
5.  单击**扫描**。  
  
    将显示扫描页。 这将显示已发现的数据库和搜索的进度。 若要停止搜索，请单击**停止**。  
  
6.  在选择文件页上，选择你想要添加到项目的数据库。  
  
    可以使用**全**并**清除所有**要选择或清除所有数据库的列表顶部的按钮。 可以按住 CTRL 键选择多个数据库，或按住 SHIFT 键以选择范围的数据库。  
  
7.  单击“下一步” 。  
  
8.  在验证页上，单击**完成**。  
  
## <a name="browsing-access-metadata"></a>浏览访问元数据  
将 Access 数据库添加到项目后，项目元数据将出现在访问元数据资源管理器。 您可以浏览数据库和资源管理器中的数据库对象的层次结构。  
  
**若要浏览元数据**  
  
1.  在访问元数据资源管理器中，展开**访问元数据库**，然后展开**数据库**。  
  
2.  展开数据库，你想要查看，然后展开**查询**。  
  
    请注意，查询列表。 如果选择一个查询， **SQL**选项卡和一个**属性**选项卡显示在右窗格中。  
  
3.  展开**表**，然后选择一个表。  
  
    请注意，显示四个选项卡：**表**，**类型映射**，**属性**，以及**数据**。  
  
4.  展开某个表中，展开**密钥**，然后选择一个密钥。  
  
    在右窗格中显示的键属性。  
  
5.  展开**索引**，然后选择索引。  
  
    在右窗格中显示索引属性。  
  
## <a name="refreshing-databases"></a>正在刷新数据库  
如果 Access 数据库发生更改后添加其文件，您可以更新从 Access 数据库的元数据。  
  
**若要更新访问元数据**  
  
-   在访问元数据资源管理器中，右键单击该数据库，然后选择**从数据库刷新**。  
  
## <a name="removing-databases"></a>删除数据库  
通过执行以下步骤，可以从项目中删除访问数据库。  
  
**若要从项目中删除数据库**  
  
1.  在访问元数据资源管理器中，展开**访问元数据库**，然后展开**数据库**。  
  
2.  右键单击数据库，然后依次**Remove Database**。  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是[连接到 SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)。  
  
## <a name="see-also"></a>请参阅  
[Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[创建和管理项目](creating-and-managing-projects-accesstosql.md)  
  
