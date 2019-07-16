---
title: 转换数据库对象加载到 SQL Server (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac993a6d-0283-4823-8793-6b217677dfa3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: a6966209300e6959e7ba9cb1afa11eb42b855d82
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909014"
---
# <a name="loading-converted-database-objects-into-sql-server-mysqltosql"></a>将转换数据库对象加载到 SQL Server (MySQLToSQL)
转换为的 MySQL 数据库后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，您可以加载到生成的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 您既可以让 SSMA 创建对象，也可以编写对象脚本并自行运行这些脚本。 SSMA 此外，还允许使用的实际内容更新目标元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 数据库。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同步和脚本之间进行选择  
如果你想要将已转换的数据库对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]也无需修改的 SQL Azure，可以让 SSMA 直接创建或重新创建数据库对象。 方法的过程快速而简单，但不允许对自定义的 TRANSACT-SQL 代码定义[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象。  
  
如果你想要修改用于创建对象，Transact SQL 或如果想要更好地控制对象的创建，使用 SSMA 创建脚本。 可以然后修改这些脚本，每个对象分别创建，并甚至使用 SQL Server 代理来计划创建这些对象。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>使用 SSMA 来与 SQL Server 中同步对象  
若要使用 SSMA 创建 SQL Server 或 SQL Azure 数据库对象，您选择的对象中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 元数据资源管理器，然后再同步的对象与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，如下面的过程中所示。 默认情况下，如果对象已经存在于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，并且如果 SSMA 元数据具有某些本地更改或对这些非常对象的定义更新 SSMA 会更改中的对象定义[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 您可以通过编辑更改默认行为**项目设置**。  
  
> [!NOTE]  
> 可以选择现有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或未转换从 MySQL 数据库的 SQL Azure 数据库对象。 但是，不会重新创建或更改 SSMA 这些对象。  
  
##### <a name="to-synchronize-objects-with-sql-server-or-sql-azure"></a>若要使用 SQL Server 或 SQL Azure 同步对象  
  
1.  在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 元数据资源管理器中，展开顶部[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 节点，然后展开**数据库**。  
  
2.  选择要处理的对象：  
  
    -   若要同步整个数据库，选择数据库名称旁边的复选框。  
  
    -   以同步或省略了单个对象的类别，选择或清除的对象或文件夹旁边的复选框。  
  
3.  选择要在 SQL Server 或 SQL Azure 元数据资源管理器中处理的对象后，右键单击**数据库**，然后单击**与数据库同步**。  
  
    你还可以通过右键单击该对象或其父文件夹，然后单击同步单个对象的类别**与数据库同步**。  
  
    之后，将显示 SSMA**与数据库同步**对话框中，可以看到两组项的位置。 在左侧，SSMA 显示所选的数据库对象树中表示。 在右侧窗格中，您可以看到表示 SSMA 元数据中的相同对象的树。 您可以通过单击左侧或右侧展开树 + 按钮。 在操作列中放置两个树之间显示的同步方向。  
  
    一个操作号可以是以下三种状态：  
  
    -   向左的箭头表示元数据的内容将保存在数据库 （默认值）。  
  
    -   向右箭头意味着数据库内容将覆盖 SSMA 元数据。  
  
    -   跨登录意味着将执行任何操作。  
  
    -   单击操作的符号以更改状态。 当您单击时将执行实际同步**确定**的按钮**与数据库同步**对话框。  
  
## <a name="scripting-objects"></a>编写对象脚本  
若要保存[!INCLUDE[tsql](../../includes/tsql-md.md)]定义的转换后的数据库对象，或更改的对象定义并自己运行脚本，您可以保存转换后的数据库对象定义为[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本。  
  
**若要将对象另存为脚本**  
  
1.  选择要将保存到脚本的对象后，右键单击**数据库**，然后单击**另存为脚本**。  
  
    您还可以通过右键单击该对象或其父文件夹，然后单击脚本单个对象的类别**另存为脚本**。  
  
2.  在中**另存为**对话框框中，找到你想要保存该脚本文件中输入名称的文件夹**文件名**框中，然后[!INCLUDE[clickOK](../../includes/clickok-md.md)]SSMA 将追加.sql 文件扩展名。  
  
### <a name="modifying-scripts"></a>修改脚本  
SQL Server 或 SQL Azure 对象定义保存为脚本后，可以使用 SQL Server Management Studio 修改脚本。  
  
**若要修改的脚本**  
  
1.  在 Management Studio**文件**菜单，依次指向**打开**，然后单击**文件**。  
  
2.  在打开的对话框中，找到并选择脚本文件，并单击**确定**。  
  
3.  通过使用查询编辑器中编辑脚本文件。有关查询编辑器的详细信息，请参阅"编辑器方便命令和功能"SQL Server 联机丛书中。  
  
4.  若要保存该脚本，在文件菜单上，选择**保存**。  
  
### <a name="running-scripts"></a>正在运行的脚本  
可以在 SQL Server Management Studio 中运行的脚本或单个语句。  
  
**若要运行脚本**  
  
1.  在 SQL Server Management Studio**文件**菜单，依次指向**打开**，然后单击**文件**。  
  
2.  在打开的对话框中，找到并选择脚本文件，并单击**确定**。  
  
3.  若要运行完整的脚本，请按**F5**密钥。  
  
4.  若要运行一组语句，在查询编辑器窗口中，选择语句，然后按**F5**密钥。  
  
5.  有关如何使用查询编辑器中运行脚本的详细信息，请参阅"SQL Server Management Studio-查询"SQL Server 联机丛书中。  
  
6.  你可以也运行脚本从命令行使用**sqlcmd**实用程序，并从 SQL Server 代理。 有关详细信息**sqlcmd**，请参阅 SQL Server 联机丛书中的"sqlcmd 实用程序"。 有关 SQL Server 代理的详细信息，请参阅"自动执行管理任务 （SQL Server 代理）"SQL Server 联机丛书中。  
  
## <a name="securing-objects-in-sql-server"></a>保护 SQL Server 中的对象  
你已加载到 SQL Server 的已转换的数据库对象后，您可以授予和拒绝对这些对象的权限。 它是一个好办法迁移之前执行此操作与 SQL Server 的数据。 有关如何帮助保护 SQL Server 中的对象的信息，请参阅"安全注意事项的数据库和数据库应用程序"SQL Server 联机丛书中。  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是[将 MySQL 数据迁移到 SQL Server-Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
## <a name="see-also"></a>请参阅  
[迁移 MySQL 数据库移到 SQL Server-Azure SQL 数据库&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
