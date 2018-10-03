---
title: 开始使用用于访问 SQL Server 迁移助手 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- error list pane
- getting started
- menus
- metadata explorers
- output pane
- toolbars
- user interface
- user interface overview
ms.assetid: 462a731f-08f1-44e1-9eeb-4deac6d2f6c5
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 1168609d35a266f2ac5fe6641aee7ca131bc9d89
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668665"
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>开始使用 SQL Server Migration Assistant for Access (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) 进行访问，可快速将转换到访问数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 对象，将上传到生成的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，并将数据迁移从 Access 到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 如果有必要，你还可以链接到访问表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 的表，以便可以继续使用现有访问前端应用程序与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。  
  
本主题介绍安装过程，并可帮助你熟悉 SSMA 用户界面。  
  
## <a name="installing-ssma"></a>安装 SSMA  
若要使用 SSMA，您首先必须安装 SSMA 客户端程序可以访问你想要迁移的这两个数据库的计算机和目标实例上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 有关安装说明，请参阅[安装 SQL Server Migration Assistant for Access &#40;AccessToSQL&#41;](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md)。  
  
若要启动 SSMA，请单击**启动**，依次指向**所有程序**，指向**SQL Server Migration Assistant for Access**，然后选择**SQL Server 迁移适用于访问助手**。  
  
## <a name="using-ssma"></a>使用 SSMA  
安装 SSMA 之后，它有助于熟悉 SSMA 用户界面使用该工具将访问数据库迁移到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 SSMA 用户界面，包括元数据资源管理器、 元数据、 工具栏、 输出窗格中，和错误列表窗格显示下面的关系图：  
  
![用于访问图形用户界面的 SSMA](../../ssma/access/media/ssmaforaccessgui.gif "用于访问图形用户界面的 SSMA")  
  
若要开始迁移，创建一个新项目，并将 Access 数据库添加到元数据资源管理器中访问。 然后可以右键单击对象访问元数据资源管理器中执行以下任务：
- 导出到访问数据库对象的清单[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。
- 创建评估转换到的报表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。
- 转换到访问架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 架构。

此外可以使用工具栏和菜单来执行这些任务。  
  
您还必须连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 成功连接时，层次结构后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库将出现在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器。 转换为 Access 架构后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架构，您可以选择这些转换后的架构中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器，然后将加载到架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
如果选择了 Azure SQL DB 从迁移到新项目对话框中的下拉列表中，您必须连接到 Azure SQL DB。 成功连接后，Azure SQL DB 数据库的层次结构将显示在 Azure SQL DB 元数据资源管理器中。 将 Access 架构转换为 Azure SQL DB 架构后，可以在 Azure SQL DB 元数据资源管理器中选择这些转换后的架构，然后加载到架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
加载到转换后的架构后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]也可以返回到访问元数据资源管理器并将数据从 Access 数据库复制到迁移的 Azure SQL DB[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 数据库。 如果有必要，你还可以链接到访问表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 的表。  
  
有关这些任务以及如何执行这些详细信息，请参阅以下主题：  
  
-   [为迁移准备 Access 数据库](preparing-access-databases-for-migration-accesstosql.md)  
  
-   [Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
-   [链接到 SQL Server 访问应用程序](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
以下各节介绍 SSMA 用户界面的功能。  
  
### <a name="metadata-explorers"></a>元数据资源管理器  
SSMA 包含两个元数据资源管理器可用于浏览和执行操作的访问权限和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 数据库。  
  
#### <a name="access-metadata-explorer"></a>访问元数据资源管理器  
访问元数据资源管理器中显示已添加到项目的访问数据库的相关信息。 添加 Access 数据库，SSMA 检索有关该数据库，这是可访问元数据资源管理器中的元数据的元数据。  
  
访问元数据资源管理器可用于执行以下任务：  
  
-   浏览每个访问数据库中的表。  
  
-   选择要转换的对象并将转换到的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法。 有关详细信息，请参阅[转换访问数据库对象](converting-access-database-objects-accesstosql.md)。  
  
-   选择数据迁移的对象和数据从这些对象迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[迁移到 SQL Server 访问数据](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)。  
  
-   链接和取消链接访问和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server 或 Azure SQL DB 元数据资源管理器  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL DB 元数据资源管理器显示的实例有关的信息或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 当您连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB、 SSMA 检索该实例的相关元数据并将其存储在项目文件中。  
  
可以使用 SQL Server 或 Azure SQL DB 元数据资源管理器来选择转换后的访问数据库对象和加载 （同步） 的实例到这些对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。  
  
有关详细信息，请参阅[加载到 SQL Server 转换数据库对象](loading-converted-database-objects-into-sql-server-accesstosql.md)。  
  
### <a name="metadata"></a>元数据  
每个元数据资源管理器右侧是描述所选的对象的选项卡。 例如，如果访问元数据资源管理器中选择一个表，四个选项卡将显示：**表**，**类型映射**，**属性**，以及**数据**. 如果您选择的表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器中，会显示三个选项卡：**表**， **SQL**，并且**数据**。  
  
大多数元数据设置是只读的。 但是，可以更改以下元数据：  
  
-   在访问元数据资源管理器中，您可以改变类型映射。 请确保进行这些更改之前创建的报表或将架构转换。  
  
-   在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器，您可以在更改表和索引属性**表**选项卡。进行这些更改之前加载到架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[转换访问数据库对象](converting-access-database-objects-accesstosql.md)。  
  
### <a name="toolbars"></a>工具栏  
SSMA 具有两个工具栏： 项目工具栏和迁移工具栏。  
  
#### <a name="the-project-toolbar"></a>项目工具栏  
项目工具栏包含用于处理项目、 添加 Access 数据库文件，以及连接到的按钮[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 这些按钮上类似于命令**文件**菜单。  
  
#### <a name="the-migration-toolbar"></a>迁移工具栏  
迁移工具栏包含以下命令：  
  
|Button|函数|  
|----------|------------|  
|**转换、加载和迁移**|转换 Access 数据库时，将加载到已转换的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，并将迁移到数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，所有在一个步骤中。|  
|**创建报表**|将转换为所选的访问架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 语法，然后创建一个报表来显示如何成功转换了。<br /><br />仅当在访问元数据资源管理器中选择对象时，此命令才可用。|  
|**转换架构**|将转换为所选的访问架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 架构。<br /><br />仅当在访问元数据资源管理器中选择对象时，此命令才可用。|  
|**将数据迁移**|将数据迁移到 Access 数据库从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 在运行此命令之前，必须将转换到 Access 架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 架构，然后将加载到对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。<br /><br />仅当在访问元数据资源管理器中选择对象时，此命令才可用。|  
|**停止**|停止当前进程，例如，将转换为对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 语法。|  
  
### <a name="menus"></a>菜单  
SSMA 包含以下菜单：  
  
|菜单|Description|  
|--------|---------------|  
|**File**|迁移向导，处理项目，添加和删除访问权限的数据库文件，以及连接到包含命令[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。|  
|**编辑**|包含用于查找和使用中的详细信息页面，如将复制的文本命令[!INCLUDE[tsql](../../includes/tsql-md.md)]SQL 的详细信息窗格中。 若要打开**管理书签**对话框中的，在编辑菜单上单击管理书签。 在对话框中，您将看到一个现有书签列表。 可以使用对话框右侧的按钮来管理书签。|  
|**“视图”**|包含**同步元数据资源管理器**命令。 这会同步访问元数据资源管理器之间的对象和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 元数据资源管理器。 此外包含用于显示和隐藏命令**输出**并**错误列表**窗格和一个选项**布局**使用布局进行管理。|  
|**工具**|包含命令以创建报表、 导出数据、 将对象和数据迁移，链接表，并提供的全局访问权限和项目设置对话框。|  
|**帮助**|提供访问到 SSMA 帮助和**有关**对话框。|  
  
### <a name="output-pane-and-error-list-pane"></a>输出窗格和错误列表窗格  
**视图**菜单提供用于切换的可见性输出窗格和错误列表窗格中的命令：  
  
-   输出窗格显示在对象转换、 对象同步和数据迁移期间从 SSMA 状态消息。  
  
-   错误列表窗格可以进行排序的列表中显示错误、 警告和信息性消息。  
  
## <a name="see-also"></a>另请参阅  
[Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
