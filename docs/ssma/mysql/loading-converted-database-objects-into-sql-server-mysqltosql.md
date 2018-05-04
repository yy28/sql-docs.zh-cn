---
title: 加载转换到 SQL Server (MySQLToSQL) 数据库对象 |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ac993a6d-0283-4823-8793-6b217677dfa3
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c20f8a262c12800b8ffa4f91bbd961f889eddcea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="loading-converted-database-objects-into-sql-server-mysqltosql"></a>加载转换到 SQL Server (MySQLToSQL) 数据库对象
转换到的 MySQL 数据库后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，你可以将生成数据库对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您可以让 SSMA 创建对象，或可以编写对象脚本时，还可以自行运行脚本。 此外，SSMA 使你可以更新目标元数据的实际内容[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同步和脚本之间进行选择  
如果你想要将已转换的数据库对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或者无需修改的 SQL Azure，您可以使用 SSMA 直接创建或重新创建数据库对象。 方法是快速而简单，但不允许的 Transact SQL 代码的定义的自定义项[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象。  
  
如果你想要修改用于创建对象，Transact SQL 或所需对象创建的更好地控制，请使用 SSMA 创建脚本。 你可以然后修改这些脚本，每个对象单独创建，甚至使用 SQL Server 代理来计划创建这些对象。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>使用 SSMA 具有 SQL Server 对象进行同步  
若要使用 SSMA 创建 SQL Server 或 SQL Azure 数据库对象，你可以选择中的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据资源管理器，然后将同步的对象与[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，如下面的过程中所示。 默认情况下，如果对象已经存在于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，如果 SSMA 元数据具有某些本地更改或更新了这些非常对象的定义，则 SSMA 将 alter 中的对象定义[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 你可以通过编辑更改默认行为**项目设置**。  
  
> [!NOTE]  
> 你可以选择现有[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或多个未转换从 MySQL 数据库的 SQL Azure 数据库对象。 但是，不会重新创建或更改的 SSMA 这些对象。  
  
##### <a name="to-synchronize-objects-with-sql-server-or-sql-azure"></a>若要使用 SQL Server 或 SQL Azure 同步对象  
  
1.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据资源管理器，展开顶部[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 节点，然后展开**数据库**。  
  
2.  选择要处理的对象：  
  
    -   若要同步整个数据库，选择数据库名称旁边的复选框。  
  
    -   若要同步或忽略单个对象的类别，选择或清除的对象或文件夹旁边的复选框。  
  
3.  选择要在 SQL Server 或 SQL Azure 元数据资源管理器中处理的对象后，右键单击**数据库**，然后单击**与数据库的同步**。  
  
    你还可以通过右键单击对象或其父文件夹，然后单击同步单个对象的类别**与数据库的同步**。  
  
    之后，将显示 SSMA**与数据库的同步**对话框中，可以看到两个项的组的位置。 在左侧，SSMA 显示在树中表示的所选的数据库对象。 在右侧，你可以看到表示 SSMA 元数据中的相同对象树。 你可以通过单击左或向右展开树 + 按钮。 同步方向放置在两个树之间的操作列所示。  
  
    一个操作符号可以处于以下三种状态：  
  
    -   向的左键意味着元数据的内容将保存在数据库 （默认值）。  
  
    -   右箭头意味着数据库内容将覆盖 SSMA 元数据。  
  
    -   交叉登录意味着将执行任何操作。  
  
    -   单击以更改状态的操作符号。 当你单击时，将执行实际同步**确定**按钮**与数据库的同步**对话框。  
  
## <a name="scripting-objects"></a>编写对象脚本  
若要保存[!INCLUDE[tsql](../../includes/tsql_md.md)]定义的转换后的数据库对象，或更改的对象定义和自己运行脚本，你可以保存转换后的数据库对象定义到[!INCLUDE[tsql](../../includes/tsql_md.md)]脚本。  
  
**若要将对象另存为脚本**  
  
1.  选择要将保存到脚本的对象后，右键单击**数据库**，然后单击**将另存为脚本**。  
  
    你还可以通过右键单击对象或其父文件夹，然后单击脚本单个对象的类别**将另存为脚本**。  
  
2.  在**另存为**对话框框中，找到你想要保存该脚本中，输入中的文件名称的文件夹**文件名**框中，然后[!INCLUDE[clickOK](../../includes/clickok_md.md)]SSMA 将追加.sql 文件扩展名。  
  
### <a name="modifying-scripts"></a>修改脚本  
SQL Server 或 SQL Azure 对象定义保存为脚本后，你可以使用 SQL Server Management Studio 修改脚本。  
  
**若要修改的脚本**  
  
1.  在 Management Studio**文件**菜单上，指向**打开**，然后单击**文件**。  
  
2.  在打开的对话框中，找到并选择你的脚本文件，然后单击**确定**。  
  
3.  通过使用查询编辑器中编辑的脚本文件。关于查询编辑器的详细信息，请参阅"编辑器方便命令和功能"SQL Server 联机丛书中。  
  
4.  若要保存该脚本中，在文件菜单上，选择**保存**。  
  
### <a name="running-scripts"></a>运行脚本  
可以在 SQL Server Management Studio 中运行的脚本或单个语句。  
  
**若要运行脚本**  
  
1.  在 SQL Server Management Studio**文件**菜单上，指向**打开**，然后单击**文件**。  
  
2.  在打开的对话框中，找到并选择你的脚本文件，然后单击**确定**。  
  
3.  若要运行的完整脚本，按**F5**密钥。  
  
4.  若要运行一组语句，在查询编辑器窗口中，选择语句，，然后按**F5**密钥。  
  
5.  有关如何使用查询编辑器来运行脚本的详细信息，请参阅"SQL Server Management Studio TRANSACT-SQL 查询"SQL Server 联机丛书中。  
  
6.  你可以还使用运行脚本从命令行**sqlcmd**实用工具和从 SQL Server 代理。 有关详细信息**sqlcmd**，请参阅 SQL Server 联机丛书中的"sqlcmd 实用工具"。 有关 SQL Server 代理的详细信息，请参阅"自动化管理任务 （SQL Server 代理）"SQL Server 联机丛书中。  
  
## <a name="securing-objects-in-sql-server"></a>保护 SQL Server 中的对象  
转换后的数据库对象加载到 SQL Server 后，您可以授予和拒绝对这些对象的权限。 它是一个好办法执行此操作在迁移之前到 SQL Server 的数据。 有关如何帮助保护 SQL Server 中的对象的信息，请参阅"安全注意事项的数据库和数据库应用程序"SQL Server 联机丛书中。  
  
## <a name="next-step"></a>下一步  
迁移过程的下一步是[将 MySQL 数据迁移到 SQL Server 的 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
## <a name="see-also"></a>另请参阅  
[迁移的 MySQL 数据库移到 SQL Server 的 Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
