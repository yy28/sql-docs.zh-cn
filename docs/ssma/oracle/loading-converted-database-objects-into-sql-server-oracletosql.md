---
title: 转换数据库对象加载到 SQL Server (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Synchronization, Securing Objects in SQL Server
- Synchronization,Scripting Objects
ms.assetid: a8ae33b2-1883-4785-922b-ea0e31c0b37a
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: fa7e74d94fba34ebb3ae1e11ccaae308dd14e3e8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685255"
---
# <a name="loading-converted-database-objects-into-sql-server-oracletosql"></a>将转换数据库对象加载到 SQL Server (OracleToSQL)
Oracle 架构转换为 SQL Server 后，可以加载到 SQL Server 生成的数据库对象。 您既可以让 SSMA 创建对象，也可以编写对象脚本并自行运行这些脚本。 此外，SSMA 可以使用 SQL Server 数据库的实际内容更新目标元数据。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同步和脚本之间进行选择  
如果你想要加载到 SQL Server 的已转换的数据库对象，而无需修改，您可以直接创建或重新创建数据库对象的 SSMA。 方法的过程快速而简单，但不允许的自定义项[!INCLUDE[tsql](../../includes/tsql-md.md)]定义存储过程以外的 SQL Server 对象的代码。  
  
如果你想要修改[!INCLUDE[tsql](../../includes/tsql-md.md)]用于创建对象，或如果想要更好地控制对象的创建，使用 SSMA 来创建脚本。 可以然后修改这些脚本，每个对象分别创建，并甚至使用 SQL Server 代理来计划创建这些对象。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>使用 SSMA 来与 SQL Server 中同步对象  
若要使用 SSMA 创建 SQL Server 数据库对象，SQL Server 元数据资源管理器中，选择的对象，然后使用 SQL Server，同步对象，如下面的过程中所示。 默认情况下，如果对象已存在 SQL Server 中和 SSMA 元数据是 SQL Server 中的对象比新 SSMA 会更改 SQL Server 中的对象定义。 您可以通过编辑更改默认行为**项目设置**。  
  
> [!NOTE]  
> 可以选择从 Oracle 数据库未转换的现有 SQL Server 数据库对象。 但是，不会重新创建或更改 SSMA 这些对象。  
  
**若要使用 SQL Server 中同步对象**  
  
1.  SQL Server 元数据资源管理器中，展开顶部的 SQL Server 节点，然后再展开**数据库**。  
  
2.  选择要处理的对象：  
  
    -   若要同步整个数据库，选择数据库名称旁边的复选框。  
  
    -   以同步或省略了单个对象的类别，选择或清除的对象或文件夹旁边的复选框。  
  
3.  选择要在 SQL Server 元数据资源管理器中处理的对象后，右键单击**数据库**，然后单击**与数据库同步**。  
  
    你还可以通过右键单击该对象或其父文件夹，然后单击同步单个对象的类别**与数据库同步**。  
  
    之后，将显示 SSMA**与数据库同步**对话框中，可以看到两组项的位置。 在左侧，SSMA 显示所选的数据库对象树中表示。 在右侧窗格中，您可以看到表示 SSMA 元数据中的相同对象的树。 您可以通过单击左侧或右侧展开树 + 按钮。 在操作列中放置两个树之间显示的同步方向。  
  
    一个操作号可以有三种状态：  
  
    -   向左的箭头表示元数据的内容将保存在数据库 （默认值）。  
  
    -   向右箭头意味着数据库内容将覆盖 SSMA 元数据。  
  
    -   跨登录意味着将执行任何操作。  
  
单击操作的符号以更改状态。 当您单击时将执行实际同步**确定**的按钮**与数据库同步**对话框。  
  
## <a name="scripting-objects"></a>编写对象脚本  
若要保存[!INCLUDE[tsql](../../includes/tsql-md.md)]定义的转换后的数据库对象，或更改的对象定义并自己运行脚本，您可以保存转换后的数据库对象定义为[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本。  
  
**若要将对象另存为脚本**  
  
1.  选择要将保存到脚本的对象后，右键单击**数据库**，然后单击**另存为脚本**。  
  
    您还可以通过右键单击该对象或其父文件夹，然后单击脚本单个对象的类别**另存为脚本**。  
  
2.  在中**另存为**对话框框中，找到你想要保存该脚本文件中输入名称的文件夹**文件名**框，并单击确定 SSMA 将追加.sql 文件扩展名。  
  
### <a name="modifying-scripts"></a>修改脚本  
已保存 SQL Server 对象定义为一个或多个脚本后，可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]可以查看和修改脚本。  
  
**若要修改的脚本**  
  
1.  上[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**文件**菜单中，依次指向**打开**，然后单击**文件**。  
  
2.  在中**打开**对话框中，选择你的脚本文件，然后单击确定。
  
3.  通过使用查询编辑器中编辑脚本文件。  
  
    有关查询编辑器的详细信息，请参阅"编辑器方便命令和功能"SQL Server 联机丛书中。  
  
4.  若要保存该脚本，在文件菜单上单击**保存**。  
  
### <a name="running-scripts"></a>正在运行的脚本  
可以在运行脚本或单个语句[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
**若要运行脚本**  
  
1.  上[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**文件**菜单中，依次指向**打开**，然后单击**文件**。  
  
2.  在中**打开**对话框中，选择你的脚本文件，然后单击确定  
  
3.  若要运行完整的脚本，请按**F5**密钥。  
  
4.  若要运行一组语句，在查询编辑器窗口中，选择语句，然后按**F5**密钥。  
  
有关如何使用查询编辑器中运行脚本的详细信息，请参阅"[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]查询"SQL Server 联机丛书中。  
  
你可以也运行脚本从命令行使用**sqlcmd**实用程序，并从 SQL Server 代理。 有关详细信息**sqlcmd**，请参阅 SQL Server 联机丛书中的"sqlcmd 实用程序"。 有关 SQL Server 代理的详细信息，请参阅"自动执行管理任务 （SQL Server 代理）"SQL Server 联机丛书中。  
  
## <a name="securing-objects-in-sql-server"></a>保护 SQL Server 中的对象  
你已加载到 SQL Server 的已转换的数据库对象后，您可以授予和拒绝对这些对象的权限。 它是一个好办法迁移之前执行此操作与 SQL Server 的数据。 有关如何帮助保护 SQL Server 中的对象的信息，请参阅"安全注意事项的数据库和数据库应用程序"SQL Server 联机丛书中。  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是[将数据迁移到 SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>请参阅  
[迁移的 Oracle 数据库移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
