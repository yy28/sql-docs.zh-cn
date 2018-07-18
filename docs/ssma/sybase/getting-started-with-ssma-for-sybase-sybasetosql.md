---
title: 用于 SAP ASE (SybaseToSQL) 入门 SSMA |Microsoft 文档
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: eb7ace0b83cdb4277a742c9932430fedf7b3e532
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34779273"
---
# <a name="getting-started-with-ssma-for-sap-ase-sybasetosql"></a>用于 SAP ASE (SybaseToSQL) 入门 SSMA
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) 的 SAP ASE 使你能够快速地转换到的 SAP 自适应 Server Enterprise (ASE) 数据库架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库架构，上载生成架构转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库，并从中迁移数据到 SAP ASE[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。  
  
本主题介绍安装过程中，然后帮助你熟悉 SSMA 用户界面。  
  
## <a name="installing-and-licensing-ssma"></a>安装和许可 SSMA  
若要使用 SSMA，首先必须安装 SSMA 客户端程序可以访问两个 SAP ASE 的源实例和目标实例的计算机上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。 若要使用服务器端数据迁移，你必须安装扩展包和至少一个 SAP ASE 提供程序 （OLE DB 或 ADO.NET） 正在运行的计算机上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 这些组件支持数据迁移和模拟的 SAP ASE 系统函数。 有关安装说明，请参阅[安装 SSMA for SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)。  
  
若要启动 SSMA，请单击**启动**，指向**所有程序**，指向 **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Sybase 迁移助手**，然后选择 **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Sybase 迁移助手**。 第一次启动 SSMA，会出现一个授权对话框。 必须通过使用 Windows Live ID，然后才能使用 SSMA 许可证 SSMA。 授权说明中的安装说明中附带了[Sybase 客户端安装 SSMA &#40;SybaseToSQL&#41; ](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)主题。  
  
## <a name="ssma-for-sap-ase-user-interface"></a>SAP ASE 用户界面的 SSMA  
安装和许可 SSMA 后，你可以使用 SSMA SAP ASE 将数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。 它有助于熟悉 SSMA 用户界面在开始之前。 下图显示的 SSMA，包括元数据资源管理器、 元数据、 工具栏、 输出窗格中，和错误列表窗格中的用户界面：  
  
![SAP ASE 用户界面的 SSMA](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "SSMA for SAP ASE 用户界面")  
  
若要开始迁移，必须首先创建一个新的项目。 然后，你连接到 SAP ASE。 在成功连接之后, 的 SAP ASE 数据库层次结构会在 Sybase 元数据资源管理器中。 然后右键单击对象 Sybase 元数据资源管理器来执行任务，例如创建评估转换到的报表，您可以[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。 你还可以执行这些任务通过工具栏和菜单。  
  
你还必须连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。 成功连接时，层次结构之后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库将出现在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据资源管理器。 在转换到的 SAP ASE 架构后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库架构，选择这些转换后的架构中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据资源管理器，然后将加载到架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。  
  
加载转换后的架构，转换后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库，你可以返回到 Sybase 元数据资源管理器，然后将数据从 SAP ASE 数据库复制到迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。  
  
有关这些任务以及如何执行它们的详细信息，请参阅[将 SAP ASE 数据库迁移到 SQL Server 的 Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)。  
  
下列各节描述 SSMA 用户界面的功能。  
  
### <a name="metadata-explorers"></a>元数据资源管理器  
SSMA 包含两个元数据资源管理器来浏览和 SAP ASE 上执行操作和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。  
  
#### <a name="sybase-metadata-explorer"></a>Sybase 元数据资源管理器  
Sybase 元数据资源管理器中显示 SAP ASE 的源实例上的数据库的相关信息。  
  
通过使用 Sybase 元数据资源管理器，你可以执行以下任务：  
  
-   浏览每个数据库中的表。  
  
-   选择要转换的对象，然后将转换到的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL Database 语法。 有关详细信息，请参阅[转换 SAP ASE 数据库对象&#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)。  
  
-   选择用于数据迁移的对象，然后将数据迁移到这些对象从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。 有关详细信息，请参阅[到 SQL Server 的 Azure SQL 数据库迁移 SAP ASE 数据&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md)。  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>SQL Server 或 SQL Azure 元数据资源管理器  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SQL Azure 元数据资源管理器显示的实例有关的信息或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。 当您连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库，SSMA 中检索该实例的相关元数据并将其存储在项目文件中。  
  
你可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据资源管理器来选择转换后的 SAP ASE 数据库对象，然后加载 （同步） 的实例的那些对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。  
  
有关详细信息，请参阅[加载到 SQL Server 转换数据库对象&#40;SybaseToSQL&#41;](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md)。  
  
### <a name="metadata"></a>元数据  
每个元数据资源管理器右侧是描述所选的对象的选项卡。 例如，如果 Sybase 元数据资源管理器中选择的表，六个选项卡将显示：**表**， **SQL**，**类型映射**，**数据**， **属性**，和**报表**。 **报表**仅在创建包含所选的对象的报表之后，选项卡包含的信息。 如果你选择的表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据资源管理器中，三个选项卡显示：**表**， **SQL**，和**数据**。  
  
大多数元数据设置是只读的。 但是，你可以更改以下元数据：  
  
-   在 Sybase 元数据资源管理器，可以修改过程，类型映射。 在转换架构之前，请进行这些更改。  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据资源管理器中，你可以更改[!INCLUDE[tsql](../../includes/tsql_md.md)]的存储过程。 进行这些更改，在加载到架构之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
在元数据资源管理器所做的更改将反映在项目元数据，不在源或目标数据库中。  
  
### <a name="toolbars"></a>工具栏  
SSMA 具有两个工具栏： 项目工具栏和迁移工具栏。  
  
#### <a name="the-project-toolbar"></a>项目工具栏  
项目工具栏包含用于处理项目、 连接到 SAP ASE 和连接到的按钮[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。 这些按钮上类似于命令**文件**菜单。  
  
#### <a name="the-migration-toolbar"></a>迁移工具栏  
迁移工具栏包含以下命令：  
  
|按钮|函数|  
|----------|------------|  
|**创建报表**|将转换到所选的 SAP ASE 对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法，然后创建一个报表来显示如何成功转换了。<br /><br />仅当 Sybase 元数据资源管理器中选择对象时，此命令时可用。|  
|**转换架构**|将转换到所选的 SAP ASE 对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库对象。<br /><br />仅当 Sybase 元数据资源管理器中选择对象时，此命令时可用。|  
|**迁移数据**|将数据迁移从 SAP ASE 数据库到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。 在运行此命令之前，必须将转换到的 SAP ASE 架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库架构，然后将加载到对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。<br /><br />仅当 Sybase 元数据资源管理器中选择对象时，此命令时可用。|  
|**停止**|停止当前进程，如转换到的对象处理[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL Database 语法。|  
  
### <a name="menus"></a>菜单  
SSMA 包含以下菜单：  
  
|菜单|Description|  
|--------|---------------|  
|**File**|包含用于处理项目、 连接到 SAP ASE 和连接到的命令[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库。|  
|**编辑**|包含用于查找和处理的详细信息页中，如将复制的文本命令[!INCLUDE[tsql](../../includes/tsql_md.md)]从 SQL 详细信息窗格。 此外包含**管理书签**选项，其中你可以看到的现有书签列表。 可以使用对话框右侧的按钮来管理在书签。|  
|**“视图”**|包含**同步元数据资源管理器**命令。 这将同步 Sybase 元数据资源管理器之间的对象和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据资源管理器。 此外包含用于显示和隐藏的命令**输出**和**错误列表**窗格和一个选项**布局**管理两种布局。|  
|**工具**|包含命令以创建报表、 导出数据，并将对象和数据迁移。 此外提供对访问**全局设置**和**项目设置**对话框。|  
|**测试人员**|包含命令以创建测试用例、 查看测试结果和用于数据库备份管理命令。|  
|**帮助**|提供访问到 SSMA 帮助和**有关**对话框。|  
  
### <a name="output-pane-and-error-list-pane"></a>输出窗格中和错误列表窗格  
**视图**菜单提供用于切换的可见性输出窗格和错误列表窗格的命令：  
  
-   输出窗格显示在对象转换、 对象同步和数据迁移期间从 SSMA 状态消息。  
  
-   错误列表窗格显示您可以进行排序的列表中错误、 警告和信息性消息。  
  
## <a name="see-also"></a>另请参阅  
[将 SAP ASE 数据库迁移到 SQL Server 的 Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[用户界面参考&#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
