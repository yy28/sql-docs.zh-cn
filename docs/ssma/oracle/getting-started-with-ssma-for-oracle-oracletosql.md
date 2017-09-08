---
title: "入门 Oracle (OracleToSQL) SSMA |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSMA for Oracle, Metadata Explorers
- SSMA for Oracle, Toolbars
ms.assetid: df79664c-972e-4bef-865a-ce609789fee7
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2ad25369dc4a9d9cc7a26795320050dcb583e92b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="getting-started-with-ssma-for-oracle-oracletosql"></a>入门 Oracle (OracleToSQL) SSMA
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) 的 Oracle 使你能够快速地转换到的 Oracle 数据库架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]架构，上载生成架构转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和将数据迁移到的 Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
本主题介绍安装过程中，然后帮助你熟悉 SSMA 用户界面。  
  
## <a name="installing-ssma"></a>安装 SSMA  
若要使用 SSMA，首先必须安装 SSMA 客户端程序可以访问源 Oracle 数据库和目标实例的计算机上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 你随后必须安装的扩展包以及至少一台 Oracle 提供程序 (OLE DB 或[!INCLUDE[vstecado](../../includes/vstecado_md.md)]) 正在运行的计算机上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 这些组件支持数据迁移和模拟的 Oracle 系统函数。 有关安装说明，请参阅[安装 SSMA for Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)。  
  
若要启动 SSMA，请单击**启动**，指向**所有程序**，指向 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for Oracle**，然后单击 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for Oracle**。  
  
## <a name="ssma-for-oracle-user-interface"></a>SSMA for Oracle 用户界面  
SSMA 安装后，你可以使用 SSMA Oracle 将数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 它有助于熟悉 SSMA 用户界面在开始之前。 下图显示的 SSMA，包括元数据资源管理器、 元数据、 工具栏、 输出窗格中，和错误列表窗格中的用户界面：  
  
![适用于 Oracle UI 的 SSMA](../../ssma/oracle/media/ssma_oracle_ui.jpg "SSMA for Oracle UI")  
  
若要开始迁移，必须首先创建一个新的项目。 然后，你连接到 Oracle 数据库。 在成功连接之后, Oracle 架构将出现在 Oracle 元数据资源管理器。 然后右键单击对象 Oracle 元数据资源管理器来执行任务，如创建评估转换到的报表，您可以[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 你可以使用工具栏和菜单来执行这些任务。  
  
你还必须连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 成功连接时，层次结构之后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库将出现在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器。 在转换到的 Oracle 架构后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]架构，选择这些转换后的架构中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器，然后同步与架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
同步具有转换后的架构后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，可以返回到 Oracle 元数据资源管理器，还可以将数据迁移到的 Oracle 架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。  
  
有关这些任务以及如何执行它们的详细信息，请参阅[将 Oracle 数据库迁移到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)。  
  
下列各节描述 SSMA 用户界面的功能。  
  
### <a name="metadata-explorers"></a>元数据资源管理器  
SSMA 包含两个元数据资源管理器浏览以及对 Oracle 执行操作和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。  
  
#### <a name="oracle-metadata-explorer"></a>Oracle 元数据资源管理器  
Oracle 元数据资源管理器显示有关 Oracle 架构的信息。 通过使用 Oracle 元数据资源管理器，你可以执行以下任务：  
  
-   浏览每个架构中的对象。  
  
-   选择要转换的对象，然后将转换到的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法。 有关详细信息，请参阅[转换 Oracle 架构 &#40; OracleToSQL &#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)。  
  
-   选择数据迁移的表，然后将数据迁移到这些表从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 有关详细信息，请参阅[将 Oracle 数据迁移到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md)。  
  
#### <a name="sql-server-metadata-explorer"></a>SQL 服务器元数据资源管理器  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器中显示的实例有关的信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 当您连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，SSMA 检索该实例的相关元数据，并将其存储在项目文件中。  
  
你可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器，选择转换后的 Oracle 数据库对象，并与的实例同步这些对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
有关详细信息，请参阅[加载到 SQL Server &#40; OracleToSQL &#41; 转换数据库对象](../../ssma/oracle/loading-converted-database-objects-into-sql-server-oracletosql.md)。  
  
### <a name="metadata"></a>元数据  
每个元数据资源管理器右侧是描述所选的对象的选项卡。 例如，如果选择 Oracle 元数据资源管理器中的表，将显示六个选项卡：**表**， **SQL**，**类型映射，报告**，**属性**，和**数据**。 **报表**选项卡包含的信息，只有在创建报表后，包含所选的对象。 如果你选择的表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器中，将显示三个选项卡：**表**， **SQL**，和**数据**。  
  
大多数元数据设置是只读的。 但是，你可以更改以下元数据：  
  
-   在 Oracle 元数据资源管理器，可以修改过程，类型映射。 若要转换的更改的过程和类型映射，请在转换架构之前进行更改。  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器，你可以更改[!INCLUDE[tsql](../../includes/tsql_md.md)]的存储过程。 若要查看这些更改中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，进行这些更改，在加载到架构之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
在元数据资源管理器所做的更改将反映在项目元数据，不在源或目标数据库中。  
  
### <a name="toolbars"></a>工具栏  
SSMA 具有两个工具栏： 项目工具栏和迁移工具栏。  
  
#### <a name="the-project-toolbar"></a>项目工具栏  
项目工具栏包含用于处理项目、 连接到 Oracle，并且连接到的按钮[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 这些按钮上类似于命令**文件**菜单。  
  
#### <a name="migration-toolbar"></a>迁移工具栏  
下表显示迁移工具栏命令：  
  
|按钮|函数|  
|------|--------|  
|**创建报表**|将转换到所选的 Oracle 对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法，然后创建一个报表来显示如何成功转换了。<br /><br />除非在 Oracle 元数据资源管理器中选择对象，已禁用此命令。|  
|**转换架构**|将转换到所选的 Oracle 对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象。<br /><br />除非在 Oracle 元数据资源管理器中选择对象，已禁用此命令。|  
|**迁移数据**|将数据迁移从 Oracle 数据库到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 在运行此命令之前，必须将转换到的 Oracle 架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]架构，然后将加载到对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br />除非在 Oracle 元数据资源管理器中选择对象，已禁用此命令。|  
|**停止**|停止当前的进程。|  
  
### <a name="menus"></a>菜单  
下表显示 SSMA 菜单。  
  
|菜单|Description|  
|----|-----------|  
|**文件**|包含用于处理项目、 连接到 Oracle，并且连接到的命令[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|**编辑**|包含用于查找和处理的详细信息页中，如将复制的文本命令[!INCLUDE[tsql](../../includes/tsql_md.md)]从 SQL 详细信息窗格。 此外包含**管理书签**选项，其中你将能够查看现有的书签的列表。 可以使用对话框右侧的按钮来管理在书签。|  
|**“视图”**|包含**同步元数据资源管理器**命令。 同步之间 Oracle 元数据资源管理器的对象和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器。 此外包含用于显示和隐藏的命令**输出**和**错误列表**窗格和一个选项**布局**管理两种布局。|  
|**工具**|包含用于创建报表，报表和迁移对象和数据的命令。 此外提供对访问**全局设置**和**项目设置**对话框。|  
|**测试人员**|包含用于创建和测试用例、 存储库，与备份的管理系统使用的命令。|  
|**帮助**|提供访问到 SSMA 帮助和**有关**对话框。|  
  
### <a name="output-pane-and-error-list-pane"></a>输出窗格中和错误列表窗格  
**视图**菜单提供用于切换的可见性输出窗格和错误列表窗格的命令：  
  
-   输出窗格显示在对象转换、 对象同步和数据迁移期间从 SSMA 状态消息。  
  
-   错误列表窗格可排序的列表中显示错误、 警告和信息性消息。  
  
## <a name="see-also"></a>另請參閱  
[将 Oracle 数据迁移到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md)  
[用户界面参考 &#40; OracleToSQL &#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  

