---
title: 转换数据库对象加载到 SQL Server (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Loading Converted Database Objects
ms.assetid: 4c59256f-99a8-4351-9559-a455813dbd06
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 96e2bee47c97e85421b074e870c9dab1dd46220a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63245882"
---
# <a name="loading-converted-database-objects-into-sql-server-sybasetosql"></a>将转换数据库对象加载到 SQL Server (SybaseToSQL)
转换 Sybase Adaptive Server Enterprise (ASE) 的数据库对象后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，您可以加载到生成的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 您既可以让 SSMA 创建对象，也可以编写对象脚本并自行运行这些脚本。 SSMA 此外，还允许使用的实际内容更新目标元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 数据库。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同步和脚本之间进行选择  
如果你想要将已转换的数据库对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]也无需修改的 SQL Azure，可以让 SSMA 直接创建或重新创建数据库对象。 此方法的过程快速而简单，但不允许对自定义[!INCLUDE[tsql](../../includes/tsql-md.md)]定义的代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象，而非存储过程。  
  
如果你想要修改[!INCLUDE[tsql](../../includes/tsql-md.md)]用于创建中的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，或如果想要更好地控制何时以及如何在中创建的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，使用 SSMA 创建[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本。 你可以然后修改这些脚本、 单独创建每个对象和甚至使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 代理来计划创建这些对象。  
  
## <a name="using-ssma-to-load-objects-into-sql-server-or-sql-azure"></a>使用 SSMA 对象加载到 SQL Server 或 SQL Azure  
使用 SSMA 创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 数据库对象，选择中的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 元数据资源管理器，然后再同步的对象与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，如下面的过程中所示。 默认情况下，如果对象已经存在于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，并且如果 SSMA 元数据具有某些本地更改或对这些非常对象的定义更新 SSMA 会更改中的对象定义[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 您可以通过编辑更改默认行为**项目设置**。  
  
> [!NOTE]  
> 可以选择现有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或未转换从 ASE 数据库的 SQL Azure 数据库对象。 但是，不会重新创建或更改 SSMA 这些对象。  
  
**若要使用 SQL Server 或 SQL Azure 同步对象**  
  
1.  在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 元数据资源管理器中，展开顶部[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 节点，然后展开**数据库**。  
  
2.  选择要处理的对象：  
  
    -   若要同步整个数据库，选择数据库名称旁边的复选框。  
  
    -   以同步或省略了单个对象的类别，选择或清除的对象或文件夹旁边的复选框。  
  
3.  选择要在中处理的对象后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 元数据资源管理器中，右键单击**数据库**，然后单击**与数据库同步**。  
  
    你还可以通过右键单击该对象或其父文件夹，然后单击同步单个对象的类别**与数据库同步**。  
  
    之后，将显示 SSMA**与数据库同步**对话框中，可以看到两组项的位置。 在左侧，SSMA 显示所选的数据库对象树中表示。 在右侧窗格中，您可以看到表示 SSMA 元数据中的相同对象的树。 您可以通过单击左侧或右侧展开树 + 按钮。 在操作列中放置两个树之间显示的同步方向。  
  
    一个操作号可以有三种状态：  
  
    -   向左的箭头表示元数据的内容将保存在数据库 （默认值）。  
  
    -   向右箭头意味着数据库内容将覆盖 SSMA 元数据。  
  
    -   跨登录意味着将执行任何操作。  
  
单击操作的符号以更改状态。 当您单击时将执行实际同步**确定**的按钮**与数据库同步**对话框。  
  
## <a name="scripting-objects"></a>编写对象脚本  
如果你想要保存[!INCLUDE[tsql](../../includes/tsql-md.md)]定义的转换后的数据库对象，或你想要更改的对象定义和运行编写自己的脚本，可以将已转换的数据库保存到的对象定义[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本。  
  
**若要将对象另存为脚本**  
  
1.  选择要将保存到脚本的对象后，右键单击**数据库**，然后选择**另存为脚本**。  
  
    您还可以通过右键单击该对象或其包含的文件夹，然后选择脚本单个对象的类别**保存脚本**。  
  
2.  在中**另存为**对话框框中，找到你想要保存该脚本文件中输入名称的文件夹**文件名**框中，然后依次**确定**。  
  
    SSMA 将追加.sql 文件扩展名。  
  
### <a name="modifying-scripts"></a>修改脚本  
保存后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 作为一个或多个脚本的对象定义，可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]可以查看和修改脚本。  
  
**若要修改的脚本**  
  
1.  上[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**文件**菜单中，依次指向**打开**，然后单击**文件**。  
  
2.  在中**开放**对话框中，导航到并选择你的脚本文件，然后依次**确定**。  
  
3.  编辑并使用查询编辑器的脚本文件。  
  
    有关查询编辑器的详细信息，请参阅"编辑器方便命令和功能"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
4.  若要保存该脚本，在文件菜单上，选择**保存**。  
  
### <a name="running-scripts"></a>正在运行的脚本  
可以在运行脚本或单个语句[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
**若要运行脚本**  
  
1.  上[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**文件**菜单中，依次指向**打开**，然后单击**文件**。  
  
2.  在中**开放**对话框中，导航到并选择你的脚本文件，然后依次**确定**。  
  
3.  若要运行完整的脚本，请按**F5**密钥。  
  
4.  若要运行一组语句，在查询编辑器窗口中，选择语句，然后按**F5**密钥。  
  
有关如何使用查询编辑器中运行脚本的详细信息，请参阅" [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]查询"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
你可以也运行脚本从命令行使用**sqlcmd**实用程序，并从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理。 有关详细信息**sqlcmd**，请参阅中的"sqlcmd 实用工具"[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。 有关详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理，请参阅"自动执行管理任务 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理)"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
## <a name="securing-objects-in-sql-server"></a>保护 SQL Server 中的对象  
已加载到的已转换的数据库对象后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以授予和拒绝对这些对象的权限。 它是一个好办法迁移之前执行此操作将数据到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关如何帮助保护信息对象中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅"安全注意事项的数据库和数据库应用程序"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是[迁移 Sybase ASE 数据到 SQL Server / SQL Azure(SybaseToSQL)](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)。  
  
## <a name="see-also"></a>请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
