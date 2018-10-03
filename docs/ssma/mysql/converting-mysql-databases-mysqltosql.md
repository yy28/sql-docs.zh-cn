---
title: 转换 MySQL 数据库 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8b57e41a2435d37a3408459ae30050a854cdf71a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47651705"
---
# <a name="converting-mysql-databases-mysqltosql"></a>转换 MySQL 数据库 (MySQLToSQL)
已连接到 MySQL 后，连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，并将项目设置和数据映射选项，可以将转换为的 MySQL 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 数据库对象。  
  
## <a name="the-conversion-process"></a>转换过程  
将转换数据库对象从 MySQL 所需的对象定义、 将其转换为类似[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象，再然后将此信息加载到 SSMA 元数据。 它不到的实例加载信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您然后可以通过查看对象和其属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 元数据资源管理器。  
  
在转换期间 SSMA 打印消息输出到输出窗格和错误消息为错误列表窗格。 使用的输出和错误的信息来确定是否必须修改自己的 MySQL 数据库或转换过程中，为了获取所需的转换结果。  
  
## <a name="setting-conversion-options"></a>设置转换选项  
在将对象转换之前, 查看中的项目转换选项**项目设置**对话框。 通过使用此对话框中，可以设置 SSMA 将表和索引的转换。 有关详细信息，请参阅[项目设置&#40;转换&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
## <a name="conversion-results"></a>转换结果  
下表显示哪些 MySQL 对象会转换与生成的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对象：  
  
|||  
|-|-|  
|**MySQL 对象**|**生成 SQL Server 对象**|  
|具有依赖对象，如索引的表|SSMA 创建包含依赖对象的表。 所有索引和约束与转换表。 索引转换为单独[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对象。<br /><br />**空间数据类型映射**可以仅在表节点级别执行。<br /><br />表转换设置的详细信息，请参阅[转换设置](conversion-settings-mysqltosql.md)|  
|函数|如果该函数可直接转换为 TRANSACT-SQL，SSMA 将创建一个函数。 在某些情况下，该函数必须转换为存储过程。 这可以通过使用**函数转换**项目设置中。 在这种情况下，SSMA 创建存储的过程和调用存储的过程的函数。<br /><br />**给定的选项：**<br /><br />根据项目设置将转换<br /><br />将转换为函数<br /><br />将转换为存储过程<br /><br />函数转换设置的详细信息，请参阅[转换设置](conversion-settings-mysqltosql.md)|  
|过程|如果该过程可以直接转换为 TRANSACT-SQL，SSMA 创建存储的过程。 在某些情况下必须自治事务中调用存储的过程。 SSMA 在这种情况下，创建两个存储的过程： 一个实现过程，以及用来调用实现的另一个存储过程。|  
|数据库转换|为 MySQL 对象的数据库不会直接转换的 SSMA for MySQL。 MySQL 数据库来处理更多的架构名称，然后所有物理参数在转换过程都将丢失。 使用适用于 MySQL 的 SSMA[映射到 SQL Server 架构的 MySQL 数据库&#40;MySQLToSQL&#41; ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)将映射到相应的 SQL Server 数据库/架构对 MySQL 数据库中的对象。|  
|触发器转换|**SSMA 创建触发器根据以下规则：**<br /><br />前触发器转换为 INSTEAD OF T-SQL 触发器<br /><br />AFTER 触发器将转换为带或不带行每次迭代后 T-SQL 的触发器。|  
|视图转换|SSMA 创建包含依赖对象的视图|  
|语句转换|-每个 SQL 语句对象可能包含单个 MySQL 语句 （如 DDL、 DML 和其他类型的语句） 或开始...结束块。<br />-   **多语句转换： 开始...转换结束块**SQL 语句还可以包含 BEGIN...类似于在过程、 函数或触发器定义中的结束块。 这些块都将转换为它们要转换的单个 MySQL 语句对象相同的方式。|  
  
## <a name="converting-mysql-database-objects"></a>转换 MySQL 数据库对象  
将 MySQL 数据库对象时，您首先选择你想要转换的对象，然后执行转换的 SSMA。 若要在转换期间查看输出消息上**视图**菜单中，选择**输出**。  
  
**若要将 MySQL 对象转换为 SQL Server 或 SQL Azure 的语法**  
  
1.  在 MySQL 的元数据资源管理器中，展开 MySQL 服务器，然后展开**数据库**。  
  
2.  选择要转换的对象：  
  
    -   若要将所有架构，选择复选框旁边**数据库**。  
  
    -   若要将转换或省略数据库，选择数据库名称旁边的复选框。  
  
    -   若要将转换或忽略的对象的类别，展开架构，然后选择或清除类别旁边的复选框。  
  
    -   若要将转换或忽略各个对象，展开类别文件夹，然后选择或清除的对象旁边的复选框。  
  
3.  若要将所有选定的对象的转换，请右键单击**数据库**，然后选择**转换架构**。  
  
    您还可以通过右键单击该对象或其父文件夹，然后选择转换单个对象的类别**转换架构**。  
  
## <a name="viewing-conversion-problems"></a>查看转换问题  
MySQL 的某些对象可能不会转换。 您可以查看摘要转换报告来确定转换成功率。  
  
**若要查看摘要报表**  
  
1.  在 MySQL 的元数据资源管理器中，选择**数据库**。  
  
2.  在右窗格中，选择**报表**选项卡。  
  
    此报表显示所有数据库对象的已评估或转换摘要评估的报表。 你还可以查看摘要报告为单个对象：  
  
    -   若要查看单个架构的报表，请在 MySQL 的元数据资源管理器中选择的数据库。  
  
    -   若要查看单个对象的报表，请在 MySQL 的元数据资源管理器中选择的对象。 具有转换问题的对象都有红色错误图标。  
  
对于无法转换的对象，可以查看导致转换失败的语法。  
  
**若要查看单个转换问题**  
  
1.  在 MySQL 的元数据资源管理器中，展开**数据库**。  
  
2.  展开显示红色错误图标的数据库。  
  
3.  在数据库中，展开具有红色错误图标的文件夹。  
  
4.  选择具有红色错误图标的对象。  
  
5.  在右窗格中，单击**报表**选项卡。  
  
6.  在顶部**报表**选项卡是一个下拉列表。 如果列表中显示**统计信息**，更改到所选**源**。  
  
    SSMA 显示的源代码和几个按钮，上面的代码。  
  
7.  单击**下一个问题**按钮。 这是一个红色错误图标的向右箭头。  
  
    SSMA 将突出显示第一个有问题的源代码的当前对象中找到。  
  
对于无法转换每个项，您需要确定想要使用该对象执行操作：  
  
-   可以修改要删除或修改有问题的代码的 MySQL 数据库中的对象。 若要将更新的代码加载到 SSMA，必须更新元数据。 有关详细信息，请参阅[连接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   您可以从迁移中排除对象。 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 元数据资源管理器和 MySQL 元数据资源管理器中，加载到对象之前清除项旁边的复选框[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 以及将数据从 MySQL 迁移。  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是[加载到 SQL Server 转换数据库对象&#40;MySQLToSQL&#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>请参阅  
[迁移 MySQL 数据库移到 SQL Server-Azure SQL 数据库&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
