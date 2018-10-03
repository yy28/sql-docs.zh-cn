---
title: 开始使用 SSMA for DB2 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 86a931c9132a23d9ceb3d46b48fbdce23bf76f92
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47737345"
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>开始使用 SSMA for DB2 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) 的 DB2 可以快速将转换到 DB2 数据库架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架构中，将为生成的架构上传[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并将数据从 DB2 到迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
本主题介绍安装过程中，然后帮助你熟悉 SSMA 用户界面。  
  
## <a name="installing-ssma"></a>安装 SSMA  
若要使用 SSMA，您首先必须安装 SSMA 客户端程序可以访问源 DB2 数据库和目标实例的计算机上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 正在运行的计算机上的 DB2 OLEDB 访问接口[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 这些组件支持数据迁移和 DB2 系统函数的模拟。 有关安装说明，请参阅[安装适用于 DB2 的 SSMA &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)。  
  
若要启动 SSMA，请单击**启动**，依次指向**所有程序**，指向 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for DB2**，然后单击 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]适用于 DB2 迁移助手**。  
  
## <a name="ssma-for-db2-user-interface"></a>适用于 DB2 用户界面的 SSMA  
安装 SSMA 后，可以使用 SSMA 将 DB2 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 它有助于熟悉 SSMA 用户界面在开始之前。 下图显示了用户界面的 SSMA，包括元数据资源管理器、 元数据、 工具栏、 输出窗格中，和错误列表窗格：  
  
![SSMA 用户界面](../../ssma/db2/media/ssma_db2_ui.png "SSMA 用户界面")  
  
若要开始迁移，必须首先创建一个新的项目。 然后，您连接到 DB2 数据库。 成功连接后，DB2 架构将显示在 DB2 元数据资源管理器。 然后右键单击对象，在 DB2 元数据资源管理器，以执行任务，如创建评估转换到的报表，您可以[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 此外可以使用工具栏和菜单来执行这些任务。  
  
您还必须连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 成功连接时，层次结构后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库将出现在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器。 转换 DB2 架构后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架构中，选择这些转换后的架构中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器，然后再同步与架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
同步包含转换后的架构后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以返回到 DB2 元数据资源管理器并将数据从 DB2 架构到迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  
  
有关这些任务以及如何执行这些详细信息，请参阅[将 DB2 数据库迁移到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)。  
  
以下各节介绍 SSMA 用户界面的功能。  
  
### <a name="metadata-explorers"></a>元数据资源管理器  
SSMA 包含两个元数据资源管理器来浏览和 DB2 上执行操作和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  
  
#### <a name="db2-metadata-explorer"></a>DB2 的元数据资源管理器  
DB2 的元数据资源管理器显示有关 DB2 架构的信息。 通过使用 DB2 的元数据资源管理器，可以执行以下任务：  
  
-   浏览每个架构中的对象。  
  
-   选择要转换的对象，然后将转换为对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法。 有关详细信息，请参阅[转换 DB2 架构&#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)。  
  
-   选择数据迁移的表，然后将数据迁移到这些表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[将 DB2 数据库迁移到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)。  
  
#### <a name="sql-server-metadata-explorer"></a>SQL Server 元数据资源管理器  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元数据资源管理器中显示的实例有关的信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 当您连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，SSMA 检索该实例的相关元数据，并将其存储在项目文件中。  
  
可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器中选择已转换的 DB2 数据库对象，并同步这些对象的实例与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
### <a name="metadata"></a>元数据  
每个元数据资源管理器右侧是描述所选的对象的选项卡。 例如，如果 DB2 元数据资源管理器中选择一个表，将显示六个选项卡：**表**， **SQL**，**类型映射，并报告**，**属性**，并**数据**。 **报表**选项卡只创建报表后，将包含所选的对象包含的信息。 如果您选择的表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器中，将显示三个选项卡：**表**， **SQL**，并且**数据**。  
  
大多数元数据设置是只读的。 但是，可以更改以下元数据：  
  
-   在 DB2 元数据资源管理器，可以更改过程和类型映射。 若要转换的更改后的过程和类型映射，进行更改，然后将转换的架构。  
  
-   在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器，您可以更改[!INCLUDE[tsql](../../includes/tsql-md.md)]的存储过程。 若要查看这些更改[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，进行这些更改之前加载到架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
在元数据资源管理器所做的更改反映在项目元数据，不在源或目标数据库中。  
  
### <a name="toolbars"></a>工具栏  
SSMA 具有两个工具栏： 项目工具栏和迁移工具栏。  
  
#### <a name="the-project-toolbar"></a>项目工具栏  
项目工具栏包含用于处理项目、 连接到 DB2，以及连接到的按钮[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 这些按钮上类似于命令**文件**菜单。  
  
#### <a name="migration-toolbar"></a>迁移工具栏  
下表显示了迁移工具栏命令：  
  
|Button|函数|  
|------|--------|  
|**创建报表**|将转换为所选的 DB2 对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法，然后创建一个报表来显示如何成功转换了。<br /><br />此命令将禁用 DB2 元数据资源管理器中选择对象。|  
|**转换架构**|将转换为所选的 DB2 对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对象。<br /><br />此命令将禁用 DB2 元数据资源管理器中选择对象。|  
|**将数据迁移**|将数据从 DB2 数据库移到迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在运行此命令之前，必须将转换到 DB2 架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架构，然后将加载到对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br />此命令将禁用 DB2 元数据资源管理器中选择对象。|  
|**停止**|停止当前进程。|  
  
### <a name="menus"></a>菜单  
下表显示了 SSMA 菜单。  
  
|菜单|Description|  
|----|-----------|  
|**File**|包含用于处理项目、 连接到 DB2，以及连接到命令[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**编辑**|包含用于查找和使用中的详细信息页面，如将复制的文本命令[!INCLUDE[tsql](../../includes/tsql-md.md)]SQL 的详细信息窗格中。 此外包含**管理书签**选项，其中你将能够看到的现有书签列表。 可以使用对话框右侧的按钮来管理书签。|  
|**“视图”**|包含**同步元数据资源管理器**命令。 用于将同步 DB2 元数据资源管理器之间的对象和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器。 此外包含命令以显示和隐藏**输出**并**错误列表**窗格和一个选项**布局**管理布局。|  
|**工具**|包含用于创建报表，并将对象和数据迁移命令。 此外提供访问权限**全局设置**并**项目设置**对话框。|  
|**帮助**|提供访问到 SSMA 帮助和**有关**对话框。|  
  
### <a name="output-pane-and-error-list-pane"></a>输出窗格和错误列表窗格  
**视图**菜单提供用于切换的可见性输出窗格和错误列表窗格中的命令：  
  
-   输出窗格显示在对象转换、 对象同步和数据迁移期间从 SSMA 状态消息。  
  
-   错误列表窗格显示可排序列表中的错误、 警告和信息性消息。  
  
## <a name="see-also"></a>请参阅  
[将 DB2 数据迁移到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[用户界面参考&#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
