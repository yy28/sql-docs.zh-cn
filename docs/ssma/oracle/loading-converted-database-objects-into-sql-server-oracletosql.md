---
title: "加载转换到 SQL Server (OracleToSQL) 数据库对象 |Microsoft 文档"
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
- Synchronization, Securing Objects in SQL Server
- Synchronization,Scripting Objects
ms.assetid: a8ae33b2-1883-4785-922b-ea0e31c0b37a
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6fd5616c61af419d5d2ff3134177ae296b317d57
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="loading-converted-database-objects-into-sql-server-oracletosql"></a>加载转换到 SQL Server (OracleToSQL) 数据库对象
Oracle 架构转换为 SQL Server 后，你可以加载到 SQL Server 生成的数据库对象。 您可以让 SSMA 创建对象，或可以编写对象脚本时，还可以自行运行脚本。 此外，SSMA 使你可以更新目标元数据的 SQL Server 数据库的实际内容。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同步和脚本之间进行选择  
如果你想要加载到 SQL Server 的已转换的数据库对象，而不进行修改，你可以 SSMA 直接创建或重新创建数据库对象。 方法可快速且简单，但不允许的自定义项[!INCLUDE[tsql](../../includes/tsql_md.md)]定义的 SQL Server 对象，存储过程以外的代码。  
  
如果你想要修改[!INCLUDE[tsql](../../includes/tsql_md.md)]用于创建对象，或如果你想要更好地控制对象创建使用 SSMA 创建脚本。 你可以然后修改这些脚本、 单独创建每个对象，甚至使用 SQL Server 代理计划创建这些对象。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>使用 SSMA 具有 SQL Server 对象进行同步  
若要使用 SSMA 创建 SQL Server 数据库对象，SQL 服务器元数据资源管理器，选择对象，然后使用 SQL Server，同步对象，如下面的过程中所示。 默认情况下，如果对象已经存在于 SQL Server，以及比 SQL Server 中的对象较新的 SSMA 元数据是否 SSMA 将更改 SQL Server 中的对象定义。 你可以通过编辑更改默认行为**项目设置**。  
  
> [!NOTE]  
> 你可以选择现有未转换从 Oracle 数据库的 SQL Server 数据库对象。 但是，不会重新创建或更改的 SSMA 这些对象。  
  
**若要与 SQL Server 中同步对象**  
  
1.  在 SQL Server 元数据资源管理器，展开顶部的 SQL Server 节点，然后再展开**数据库**。  
  
2.  选择要处理的对象：  
  
    -   若要同步整个数据库，选择数据库名称旁边的复选框。  
  
    -   若要同步或忽略单个对象的类别，选择或清除的对象或文件夹旁边的复选框。  
  
3.  选择要在 SQL Server 元数据资源管理器处理的对象后，右键单击**数据库**，然后单击**与数据库的同步**。  
  
    你还可以通过右键单击对象或其父文件夹，然后单击同步单个对象的类别**与数据库的同步**。  
  
    之后，将显示 SSMA**与数据库的同步**对话框中，可以看到两个项的组的位置。 在左侧，SSMA 显示在树中表示的所选的数据库对象。 在右侧，你可以看到表示 SSMA 元数据中的相同对象树。 你可以通过单击左或向右展开树 + 按钮。 同步方向放置在两个树之间的操作列所示。  
  
    一个操作符号可以处于三种状态：  
  
    -   向的左键意味着元数据的内容将保存在数据库 （默认值）。  
  
    -   右箭头意味着数据库内容将覆盖 SSMA 元数据。  
  
    -   交叉登录意味着将执行任何操作。  
  
单击以更改状态的操作符号。 当你单击时，将执行实际同步**确定**按钮**与数据库的同步**对话框。  
  
## <a name="scripting-objects"></a>编写对象脚本  
若要保存[!INCLUDE[tsql](../../includes/tsql_md.md)]定义的转换后的数据库对象，或更改的对象定义和自己运行脚本，你可以保存转换后的数据库对象定义到[!INCLUDE[tsql](../../includes/tsql_md.md)]脚本。  
  
**若要将对象另存为脚本**  
  
1.  选择要将保存到脚本的对象后，右键单击**数据库**，然后单击**将另存为脚本**。  
  
    你还可以通过右键单击对象或其父文件夹，然后单击脚本单个对象的类别**将另存为脚本**。  
  
2.  在**另存为**对话框框中，找到你想要保存该脚本中，输入中的文件名称的文件夹**文件名**中，，然后单击确定 SSMA 将追加.sql 文件扩展名。  
  
### <a name="modifying-scripts"></a>修改脚本  
已保存 SQL Server 对象定义为一个或多个脚本后，你可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]查看和修改脚本。  
  
**若要修改的脚本**  
  
1.  上[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]**文件**菜单上，指向**打开**，然后单击**文件**。  
  
2.  在**打开**对话框中，选择脚本文件，然后单击确定。
  
3.  通过使用查询编辑器中编辑的脚本文件。  
  
    关于查询编辑器的详细信息，请参阅"编辑器方便命令和功能"SQL Server 联机丛书中。  
  
4.  若要保存该脚本中，在文件菜单上单击**保存**。  
  
### <a name="running-scripts"></a>运行脚本  
你可以在运行脚本或单个语句[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]。  
  
**若要运行脚本**  
  
1.  上[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]**文件**菜单上，指向**打开**，然后单击**文件**。  
  
2.  在**打开**对话框中，选择你的脚本文件，然后单击确定  
  
3.  若要运行的完整脚本，按**F5**密钥。  
  
4.  若要运行一组语句，在查询编辑器窗口中，选择语句，，然后按**F5**密钥。  
  
有关如何使用查询编辑器来运行脚本的详细信息，请参阅"[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)]查询"SQL Server 联机丛书中。  
  
你可以还使用运行脚本从命令行**sqlcmd**实用工具和从 SQL Server 代理。 有关详细信息**sqlcmd**，请参阅 SQL Server 联机丛书中的"sqlcmd 实用工具"。 有关 SQL Server 代理的详细信息，请参阅"自动化管理任务 （SQL Server 代理）"SQL Server 联机丛书中。  
  
## <a name="securing-objects-in-sql-server"></a>保护 SQL Server 中的对象  
转换后的数据库对象加载到 SQL Server 后，您可以授予和拒绝对这些对象的权限。 它是一个好办法执行此操作在迁移之前到 SQL Server 的数据。 有关如何帮助保护 SQL Server 中的对象的信息，请参阅"安全注意事项的数据库和数据库应用程序"SQL Server 联机丛书中。  
  
## <a name="next-step"></a>下一步  
迁移过程的下一步是[将数据迁移到 SQL Server](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13)。  
  
## <a name="see-also"></a>另请参阅  
[将 Oracle 数据库迁移到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

