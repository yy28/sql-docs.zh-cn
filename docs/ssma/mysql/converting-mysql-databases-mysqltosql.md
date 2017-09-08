---
title: "将 MySQL 数据库 (MySQLToSQL) 转换 |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ee77ec5fa517bf955e3f83cb4a6540746215efb4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="converting-mysql-databases-mysqltosql"></a>将 MySQL 数据库 (MySQLToSQL) 转换
你已连接到 MySQL 后，连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 和设置项目和数据映射选项，您可以将转换为的 MySQL 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库对象。  
  
## <a name="the-conversion-process"></a>转换过程  
转换数据库对象从 MySQL 所需的对象定义，将它们转换为类似[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象，然后将此信息加载到 SSMA 元数据。 不，它不会将信息加载到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您然后可以通过查看对象及其属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据资源管理器。  
  
在转换期间，SSMA 打印消息输出到输出窗格中，并为错误列表窗格中的错误消息。 使用的输出和错误的信息来确定你是否必须修改您的 MySQL 数据库或你的转换过程，以获取所需的转换结果。  
  
## <a name="setting-conversion-options"></a>设置转换选项  
在将对象转换之前, 查看中的项目转换选项**项目设置**对话框。 通过使用此对话框中，你可以设置 SSMA 将表和索引的转换。 有关详细信息，请参阅[项目设置 &#40;转换 &#41;&#40;MySQLToSQL &#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
## <a name="conversion-results"></a>转换结果  
下表显示的 MySQL 对象转换，以及产生[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象：  
  
|||  
|-|-|  
|**MySQL 对象**|**生成的 SQL Server 对象**|  
|具有依赖的对象，如索引的表|SSMA 使用从属对象创建表。 表转换包含所有索引和约束。 索引转换为单独[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象。<br /><br />**空间数据类型映射**可以仅在表节点级别执行。<br /><br />有关表转换设置的详细信息，请参阅[转换设置](http://msdn.microsoft.com/en-us/f551cf6e-1575-4206-9cca-975b5b43a6b8)|  
|函数|如果该函数可以直接转换为 TRANSACT-SQL，SSMA 创建函数。 在某些情况下，该函数必须转换为存储过程。 这可以通过使用**函数转换**项目设置。 在这种情况下，SSMA 创建存储的过程和调用存储的过程的函数。<br /><br />**给定的选项：**<br /><br />根据项目设置将转换<br /><br />将转换为函数<br /><br />将转换为存储过程<br /><br />函数转换设置的详细信息，请参阅[转换设置](http://msdn.microsoft.com/en-us/f551cf6e-1575-4206-9cca-975b5b43a6b8)|  
|过程|如果该过程可以直接转换为 TRANSACT-SQL，SSMA 创建的存储的过程。 在某些情况下必须在自治事务中调用存储的过程。 在这种情况下，SSMA 创建两个存储的过程： 一个实现该过程中，以及用来调用实现的另一个存储过程。|  
|数据库转换|作为 MySQL 对象的数据库不直接通过转换 SSMA mysql。 MySQL 数据库来处理更多的架构名称和所有物理参数转换的过程都将丢失。 有关 MySQL 的 SSMA 使用[将 MySQL 数据库映射到 SQL Server 架构 &#40;MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)映射到相应的 SQL Server 数据库/架构对 MySQL 数据库中的对象。|  
|触发器转换|**SSMA 创建触发器基于以下规则：**<br /><br />在触发器转换到 INSTEAD OF T-SQL 触发器之前<br /><br />AFTER 触发器被转换为带有或不带每行的迭代后 T-SQL 的触发器。|  
|视图转换|SSMA 创建包含依赖对象的视图|  
|语句转换|-每个 SQL 语句对象可能包含单个 MySQL 语句 （如 DDL、 DML 和其他类型的语句） 或开始...结束块。<br />-   **多语句转换： 开始...结束块转换**SQL 语句还可以包含 BEGIN...类似于过程、 函数或触发器的定义中的结束块。 这些块都将转换为相同的方式，它们会转换为单一的 MySQL 语句对象。|  
  
## <a name="converting-mysql-database-objects"></a>转换 MySQL 数据库对象  
若要转换 MySQL 数据库对象，你首先选择你想要转换的对象，然后执行转换的 SSMA。 若要查看输出消息在转换期间上,**视图**菜单上，选择**输出**。  
  
**若要将 MySQL 对象转换为 SQL Server 或 SQL Azure 语法**  
  
1.  在 MySQL 元数据资源管理器中，展开 MySQL server，然后展开**数据库**。  
  
2.  选择要转换的对象：  
  
    -   若要转换的所有架构，选中的复选框旁边**数据库**。  
  
    -   若要将转换或省略数据库，选择数据库名称旁边的复选框。  
  
    -   若要将转换或忽略的对象的类别，展开架构，然后选择或清除的类别旁边的复选框。  
  
    -   若要将转换或省略单个对象，展开类别文件夹中，然后选择或清除该对象旁边的复选框。  
  
3.  要将所有所选的对象的转换，请右键单击**数据库**和选择**转换架构**。  
  
    您还可以通过右键单击该对象或其父文件夹，然后选择转换单个对象的类别**转换架构**。  
  
## <a name="viewing-conversion-problems"></a>查看转换问题  
某些 MySQL 对象可能不会转换。 你可以通过查看摘要转换报表来确定转换成功率。  
  
**若要查看摘要报表**  
  
1.  在 MySQL 元数据资源管理器中，选择**数据库**。  
  
2.  在右窗格中，选择**报表**选项卡。  
  
    此报表显示所有数据库对象的已评估或转换摘要评估的报表。 你还可以查看摘要报表为单个对象：  
  
    -   若要查看的报表的单个架构，请在 MySQL 元数据资源管理器中选择的数据库。  
  
    -   若要查看单个对象的报表，请在 MySQL 元数据资源管理器中选择的对象。 转换问题的对象具有红色错误图标。  
  
对于失败转换的对象，你可以查看导致转换失败的语法。  
  
**若要查看单个转换问题**  
  
1.  在 MySQL 元数据资源管理器中，展开**数据库**。  
  
2.  展开显示红色错误图标的数据库。  
  
3.  在数据库中，展开具有红色错误图标的文件夹。  
  
4.  选择具有红色错误图标的对象。  
  
5.  在右窗格中，单击**报表**选项卡。  
  
6.  在顶部**报表**选项卡是下拉列表。 如果此列表显示**统计信息**，更改选定范围向**源**。  
  
    SSMA 显示的源代码和紧邻代码之上的多个按钮。  
  
7.  单击**下一步问题**按钮。 这是一个带有向右箭头的红色错误图标。  
  
    SSMA 将突出显示当前对象中找到的第一个有问题的源代码。  
  
对于无法转换每个项，您必须确定你想要使用该对象执行操作：  
  
-   你可以修改 MySQL 数据库，可以删除或修改有问题的代码中的对象。 若要更新的代码载入 SSMA，你将需要更新的元数据。 有关详细信息，请参阅[连接到 MySQL &#40;MySQLToSQL &#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   你可以从迁移中排除对象。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据资源管理器和 MySQL 元数据资源管理器中，在加载到对象之前清除项旁边的复选框[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 和从 MySQL 迁移数据。  
  
## <a name="next-step"></a>下一步  
迁移过程的下一步是[加载到 SQL Server &#40; 转换数据库对象MySQLToSQL &#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>另请参阅  
[将 MySQL 数据库迁移到 SQL Server 的 Azure SQL DB &#40;MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

