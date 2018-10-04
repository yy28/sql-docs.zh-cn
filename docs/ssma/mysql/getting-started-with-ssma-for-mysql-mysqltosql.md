---
title: 开始使用 SSMA for MySQL (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Getting started, MySQL metadata explorer
- Getting started, SQL Server or SQL Azure metadata explorer
- Getting started,Installing and licensing
ms.assetid: 8ebfa061-be6f-4a07-923f-8dc832a82f70
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: bbfede87cf23da5e8867d33f4b8bad35b6af9c50
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47679665"
---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>SSMA for MySQL 入门 (MySQLToSQL)
SQL Server Migration Assistant (SSMA) for MySQL，可以快速将 MySQL 数据库架构转换为 SQL Server 或 Azure SQL DB 架构、 将生成的架构上传到 SQL Server 或 Azure SQL DB，并将数据从 MySQL 迁移到 SQL Server 或 Azure SQL DB。  
  
本主题介绍安装过程中，然后帮助你熟悉 SSMA 用户界面。  
  
## <a name="installing-ssma"></a>安装 SSMA  
若要使用 SSMA，您首先必须安装 SSMA 客户端程序可以访问源 MySQL 数据库和 SQL Server 或 Azure SQL DB 的目标实例的计算机上。 然后，运行 SSMA 客户端程序的计算机上安装 MySQL 提供程序 （MySQL ODBC 5.1 驱动程序 （受信任））。 有关安装说明，请参阅[安装适用于 MySQL 的 SSMA &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
  
若要启动 SSMA，请单击**启动**，依次指向**所有程序**，指向**SQL Server Migration Assistant for MySQL**，然后单击**SQL Server 迁移适用于 MySQL 助手**。  
  
## <a name="ssma-for-mysql-user-interface"></a>用于 MySQL 用户界面的 SSMA  
SSMA 是已安装和授权后，可以使用 SSMA 将 MySQL 数据库迁移到 SQL Server 或 Azure SQL DB。 它有助于熟悉 SSMA 用户界面在开始之前。 下图显示了用户界面的 SSMA，包括元数据资源管理器、 元数据、 工具栏、 输出窗格中，和错误列表窗格：  
  
![用于 MySql 图形用户界面的 SSMA](../../ssma/mysql/media/ssmaformysqlgui.gif "用于 MySql 图形用户界面的 SSMA")  
  
若要开始迁移，必须：  
  
1.  创建一个新的项目。  
  
2.  连接到 MySQL 数据库。  
  
3.  成功连接后，MySQL 架构将显示在 MySQL 的元数据资源管理器。 右键单击对象 MySQL 元数据资源管理器来执行任务，如创建评估转换为 SQL Server/Azure SQL DB 的报表。  
  
此外可以使用工具栏和菜单来执行这些任务。  
  
您还必须连接到 SQL Server 的实例。 成功连接后，SQL Server 数据库的层次结构将显示在 SQL Server 元数据资源管理器。 将 MySQL 架构转换为 SQL Server 架构后，SQL Server 元数据资源管理器中，选择这些转换后的架构，然后将与 SQL Server 的同步架构。  
  
如果选择了 Azure SQL DB 从迁移到新项目对话框中的下拉列表中，您必须连接到 Azure SQL DB。 成功连接后，Azure SQL DB 数据库的层次结构会在 Azure SQL DB 元数据资源管理器中。 将 MySQL 架构转换为 Azure SQL DB 架构后，在 Azure SQL DB 元数据资源管理器中选择这些转换后的架构，然后使用 Azure SQL DB 同步架构。  
  
使用 SQL Server 或 Azure SQL DB 同步转换后的架构后，你可以返回到 MySQL 元数据资源管理器，并将数据从 MySQL 架构迁移到 SQL Server 或 Azure SQL DB 数据库。  
  
有关这些任务以及如何执行这些详细信息，请参阅[将 MySQL 数据库迁移到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)。  
  
以下各节介绍 SSMA 用户界面的功能。  
  
### <a name="metadata-explorers"></a>元数据资源管理器  
SSMA 包含两个元数据资源管理器浏览并上 MySQL 和 SQL Server 数据库执行操作。  
  
### <a name="mysql-metadata-explorer"></a>MySQL 元数据资源管理器  
MySQL 元数据资源管理器中显示了有关 MySQL 架构的信息。 使用 MySQL 的元数据资源管理器，可以执行以下任务：  
  
-   浏览每个架构中的对象。  
  
-   选择对于转换，对象，然后将对象转换为 SQL Server 语法。 有关详细信息，请参阅[转换 MySQL 数据库&#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
-   选择数据迁移的表，然后将数据从这些表迁移到 SQL Server。 有关详细信息，请参阅[将 MySQL 数据迁移到 SQL Server-Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server 或 Azure SQL DB 元数据资源管理器  
SQL Server 或 Azure SQL DB 元数据资源管理器显示的 SQL Server 或 Azure SQL DB 实例有关的信息。 当您连接到 SQL Server 或 Azure SQL DB 的实例时，SSMA 中检索该实例的相关元数据，并将其存储在项目文件中。  
  
可以使用此元数据资源管理器来选择转换后的 MySQL 数据库对象，并与 SQL Server 或 Azure SQL DB 的实例同步这些对象。  
  
有关详细信息，请参阅[同步 (mysql 迁移到 SQL Server / Azure SQL DB)](http://msdn.microsoft.com/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
### <a name="metadata"></a>元数据  
每个元数据资源管理器右侧是描述所选的对象的选项卡。 例如，如果 MySQL 元数据资源管理器中选择一个表，九个选项卡将显示：**表**， **SQL**，**类型映射**，**数据**， **设置**，**字符集映射**， **SQL 模式**，**属性**，并且**报表**。 **报表**选项卡只创建报表后，将包含所选的对象包含的信息。 如果在 SQL Server 元数据资源管理器中选择一个表，将显示三个选项卡：**表**， **SQL**并**数据**。  
  
大多数元数据设置是只读的。 但是，可以更改以下元数据：  
  
-   在 MySQL 的元数据资源管理器中，您可以改变类型映射，字符集映射，SQL 模式。 若要转换的更改后的类型映射或字符集映射或 SQL 模式，进行更改，然后将转换的架构。  
  
-   SQL Server 元数据资源管理器中，您可以更改的表选项卡上的表和索引属性。若要查看 SQL Server 中的这些更改，进行这些更改之前架构加载到 SQL Server。  
  
在元数据资源管理器所做的更改反映在项目元数据，不在源或目标数据库中。  
  
### <a name="toolbars"></a>工具栏  
SSMA 具有两个工具栏： 项目工具栏和迁移工具栏。  
  
### <a name="the-project-toolbar"></a>项目工具栏  
项目工具栏包含用于处理项目、 连接到 MySQL，并连接到 SQL Server 或 Azure SQL DB 的按钮。 这些按钮上类似于命令**文件**菜单。  
  
### <a name="migration-toolbar"></a>迁移工具栏  
下表显示了迁移工具栏命令：  
  
|||  
|-|-|  
|**按钮**|**函数**|  
|**创建报表**|将所选的 MySQL 对象转换为 SQL Server 或 Azure SQL DB 对象，然后创建一个报表来显示如何成功转换了。<br /><br />此命令将禁用 MySQL 元数据资源管理器中选择对象。|  
|**转换架构**|将所选的 MySQL 对象转换为 SQL Server 或 Azure SQL DB 对象。<br /><br />此命令将禁用 MySQL 元数据资源管理器中选择对象。|  
|**将数据迁移**|将数据从 MySQL 数据库迁移到 SQL Server 或 Azure SQL DB。 在运行此命令之前，必须将 MySQL 架构转换为 SQL Server 或 Azure SQL DB 架构，然后将对象加载到 SQL Server 或 Azure SQL DB。<br /><br />此命令将禁用 MySQL 元数据资源管理器中选择对象。|  
|**停止**|停止当前进程。|  
  
### <a name="menus"></a>菜单  
下表显示了 SSMA 菜单。  
  
|||  
|-|-|  
|**菜单**|**Description**|  
|**File**|包含用于处理项目、 连接到 MySQL，并连接到 SQL Server 或 Azure SQL DB 命令。|  
|**编辑**|包含用于查找和使用的详细信息页中的文本命令。 若要打开**管理书签**对话框中的，在编辑菜单上单击管理书签。 在对话框中，您将看到一个现有书签列表。 可以使用对话框右侧的按钮来管理书签。|  
|**“视图”**|包含**同步元数据资源管理器**命令。 用于将同步之间 MySQL 元数据资源管理器和 SQL Server 或 Azure SQL DB 元数据资源管理器的对象。 此外包含命令以显示和隐藏**输出**并**错误列表**窗格和一个选项**布局**使用布局进行管理。|  
|**工具**|包含用于创建报表、 将架构转换、 从数据库刷新、 迁移对象和数据，和另存为脚本命令。 此外提供访问权限**全局设置、 默认项目设置**并**项目设置**对话框。|  
|**帮助**|提供访问到 SSMA 帮助和**有关**对话框。|  
  
### <a name="output-pane-and-error-list-pane"></a>输出窗格和错误列表窗格  
**视图**菜单提供用于切换的可见性输出窗格和错误列表窗格中的命令：  
  
-   输出窗格显示在对象转换、 对象同步和数据迁移期间从 SSMA 状态消息。  
  
-   错误列表窗格显示可排序列表中的错误、 警告和信息性消息。  
  
## <a name="see-also"></a>请参阅  
[用户界面参考&#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[将 MySQL 数据迁移到 SQL Server-Azure SQL 数据库&#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
