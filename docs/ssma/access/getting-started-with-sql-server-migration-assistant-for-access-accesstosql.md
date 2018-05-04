---
title: 要开始使用用于访问 SQL Server Migration Assistant |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 0865c92cd38cd5d89d0316a85e5fd1c3758b71c2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>开始使用 SQL Server Migration Assistant for Access (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) 的访问权限允许您快速将转换到的访问数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 对象上载到生成的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，并将数据迁移到的访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 如果有必要，你也可以链接到的访问表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库表，以便你可以继续使用现有访问前端应用程序与[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。  
  
本主题介绍安装过程，并有助于使您熟悉 SSMA 用户界面。  
  
## <a name="installing-ssma"></a>安装 SSMA  
若要使用 SSMA，首先必须安装 SSMA 客户端程序可以访问你想要迁移的这两个数据库的计算机和目标实例上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 有关安装说明，请参阅[安装 SQL Server Migration Assistant for Access &#40;AccessToSQL&#41;](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md)。  
  
若要启动 SSMA，请单击**启动**，指向**所有程序**，指向**SQL Server Migration Assistant for Access**，然后选择**SQL Server Migration Assistant for Access**。  
  
## <a name="using-ssma"></a>使用 SSMA  
最好使用该工具将迁移到 Access 数据库之前应熟悉 SSMA 用户界面安装后 SSMA，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 SSMA 用户界面，包括元数据资源管理器、 元数据、 工具栏、 输出窗格中，和错误列表窗格中显示在下图中：  
  
![访问图形用户界面的 SSMA](../../ssma/access/media/ssmaforaccessgui.gif "SSMA for 访问图形用户界面")  
  
若要开始迁移，创建新项目，然后添加到访问元数据资源管理器的 Access 数据库。 然后可以右键单击对象访问元数据资源管理器来执行以下任务：
- 导出到访问数据库对象的清单[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。
- 创建评估转换到的报表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。
- 转换到的访问架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 架构。

你可以使用工具栏和菜单来执行这些任务。  
  
你还必须连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 成功连接时，层次结构之后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库将出现在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器。 在转换到的访问架构后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]架构，你可以选择这些转换后的架构中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器，然后将加载到架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
如果你选择了 Azure SQL DB 从迁移到新项目对话框中的下拉列表中，你必须连接到 Azure SQL DB。 在成功连接之后, 的 Azure SQL DB 数据库层次结构将显示在 Azure SQL DB 元数据资源管理器。 将访问架构转换为 Azure SQL DB 架构后，你可以在 Azure SQL DB 元数据资源管理器中选择这些转换后的架构并且然后加载架构转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
加载转换后的架构，转换后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]也可以返回到访问元数据资源管理器并迁移到 Access 数据库中的数据的 Azure SQL DB[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 数据库。 如果有必要，你也可以链接到的访问表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库表。  
  
有关这些任务以及如何执行它们的详细信息，请参阅以下主题：  
  
-   [为迁移准备的 Access 数据库](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
-   [将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
-   [链接到 SQL Server 访问应用程序](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)  
  
下列各节描述 SSMA 用户界面的功能。  
  
### <a name="metadata-explorers"></a>元数据资源管理器  
SSMA 包含两个元数据资源管理器可用于浏览和执行访问操作和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 数据库。  
  
#### <a name="access-metadata-explorer"></a>访问元数据资源管理器  
访问元数据资源管理器中显示已添加到项目的访问数据库的相关信息。 当你将添加 Access 数据库时，SSMA 检索有关该数据库，这是可用于访问元数据资源管理器的元数据的元数据。  
  
访问元数据资源管理器可用于执行以下任务：  
  
-   浏览每个访问数据库中的表。  
  
-   选择要转换的对象并将转换到的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法。 有关详细信息，请参阅[转换访问数据库对象](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)。  
  
-   选择数据迁移的对象，然后从这些对象迁移数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 有关详细信息，请参阅[将访问数据迁移到 SQL Server](http://msdn.microsoft.com/f3b18af7-1af0-499d-a00d-a0af94895625)。  
  
-   链接和取消链接访问和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]表。  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server 或 Azure SQL DB 元数据资源管理器  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Azure SQL DB 元数据资源管理器显示的实例有关的信息或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 当您连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，SSMA 中检索该实例的相关元数据并将其存储在项目文件中。  
  
你可以使用 SQL Server 或 Azure SQL DB 元数据资源管理器来选择转换后的访问数据库对象和加载 （同步） 的实例的那些对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。  
  
有关详细信息，请参阅[加载到 SQL Server 转换数据库对象](http://msdn.microsoft.com/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba)。  
  
### <a name="metadata"></a>元数据  
每个元数据资源管理器右侧是描述所选的对象的选项卡。 例如，如果在访问元数据资源管理器选择的表，四个选项卡将显示：**表**，**类型映射**，**属性**，和**数据**。 如果你选择的表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器，三个选项卡显示：**表**， **SQL**，和**数据**。  
  
大多数元数据设置是只读的。 但是，你可以更改以下元数据：  
  
-   在访问元数据资源管理器中，你可能会改变类型映射。 请确保进行这些更改之前创建的报表或转换架构。  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器，你可以在更改表和索引属性**表**选项卡。进行这些更改，在加载到架构之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 有关详细信息，请参阅[转换访问数据库对象](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)。  
  
### <a name="toolbars"></a>工具栏  
SSMA 具有两个工具栏： 项目工具栏和迁移工具栏。  
  
#### <a name="the-project-toolbar"></a>项目工具栏  
项目工具栏包含用于处理项目、 添加 Access 数据库文件，以及连接到的按钮[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 这些按钮上类似于命令**文件**菜单。  
  
#### <a name="the-migration-toolbar"></a>迁移工具栏  
迁移工具栏包含以下命令：  
  
|按钮|函数|  
|----------|------------|  
|**转换、加载和迁移**|转换访问数据库时，转换将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，然后将迁移到的数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，全部位于一个步骤。|  
|**创建报表**|将转换到所选的访问架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 语法，然后创建一个报表来显示如何成功转换了。<br /><br />仅当访问元数据资源管理器中选择对象时，此命令时可用。|  
|**转换架构**|将转换到所选的访问架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 架构。<br /><br />仅当访问元数据资源管理器中选择对象时，此命令时可用。|  
|**迁移数据**|将数据迁移到 Access 数据库从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 在运行此命令之前，必须将转换到的访问架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 架构，然后加载到对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。<br /><br />仅当访问元数据资源管理器中选择对象时，此命令时可用。|  
|**停止**|停止当前进程，如转换到的对象处理[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 语法。|  
  
### <a name="menus"></a>菜单  
SSMA 包含以下菜单：  
  
|菜单|Description|  
|--------|---------------|  
|**文件**|迁移向导，使用项目中，添加和移除 Access 数据库文件，以及连接到包含命令[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。|  
|**编辑**|包含用于查找和处理的详细信息页中，如将复制的文本命令[!INCLUDE[tsql](../../includes/tsql_md.md)]从 SQL 详细信息窗格。 若要打开**管理书签**对话框中的，在编辑菜单上单击管理书签。 在对话框中，你将看到现有书签的列表。 可以使用对话框右侧的按钮来管理在书签。|  
|**“视图”**|包含**同步元数据资源管理器**命令。 这将同步访问元数据资源管理器之间的对象和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 元数据资源管理器。 此外包含用于显示和隐藏的命令**输出**和**错误列表**窗格和一个选项**布局**使用两种布局进行管理。|  
|**工具**|包含命令以创建报表、 导出数据、 将对象和数据迁移，链接表，并提供到全球的访问权限和项目设置对话框。|  
|**帮助**|提供访问到 SSMA 帮助和**有关**对话框。|  
  
### <a name="output-pane-and-error-list-pane"></a>输出窗格中和错误列表窗格  
**视图**菜单提供用于切换的可见性输出窗格和错误列表窗格的命令：  
  
-   输出窗格显示在对象转换、 对象同步和数据迁移期间从 SSMA 状态消息。  
  
-   错误列表窗格显示您可以进行排序的列表中错误、 警告和信息性消息。  
  
## <a name="see-also"></a>另请参阅  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
