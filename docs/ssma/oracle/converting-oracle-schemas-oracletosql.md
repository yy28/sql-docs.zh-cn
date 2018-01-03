---
title: "转换 Oracle 架构 (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Conversion Results
ms.assetid: e021182d-31da-443d-b110-937f5db27272
caps.latest.revision: "14"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.openlocfilehash: 208378f2be9ad4eea080df758616e554c1262905
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="converting-oracle-schemas-oracletosql"></a>转换 Oracle 架构 (OracleToSQL)
如果已连接到 Oracle 后，连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，并设置项目和数据映射选项，你可以将转换到的 Oracle 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库对象。  
  
## <a name="the-conversion-process"></a>转换过程  
转换数据库对象从 Oracle 获取的对象定义，并将其转换为类似[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象，然后将此信息加载到 SSMA 元数据。 不，它不会将信息加载到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您然后可以通过查看对象及其属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器。  
  
在转换期间，SSMA 打印消息输出到输出窗格中，并为错误列表窗格中的错误消息。 使用的输出和错误的信息来确定你是否必须修改您的 Oracle 数据库或您的转换过程，以获取所需的转换结果。  
  
## <a name="setting-conversion-options"></a>设置转换选项  
在将对象转换之前, 查看中的项目转换选项**项目设置**对话框。 通过使用此对话框中，你可以设置 SSMA 将函数和全局变量的转换。 有关详细信息，请参阅[项目设置 &#40;转换 &#41;&#40; OracleToSQL &#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
## <a name="conversion-results"></a>转换结果  
下表显示的 Oracle 对象转换，以及产生[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象：  
  
|||  
|-|-|  
|Oracle 对象|生成的 SQL Server 对象|  
|函数|如果该函数可以直接转换为[!INCLUDE[tsql](../../includes/tsql_md.md)]，SSMA 创建函数。<br /><br />在某些情况下，该函数必须转换为存储过程。 在这种情况下，SSMA 创建存储的过程和调用存储的过程的函数。|  
|过程|如果该过程可以直接转换为[!INCLUDE[tsql](../../includes/tsql_md.md)]，SSMA 创建的存储的过程。<br /><br />在某些情况下必须在自治事务中调用存储的过程。 在这种情况下，SSMA 创建两个存储的过程： 一个实现该过程中，以及用来调用实现的另一个存储过程。|  
|包|SSMA 创建一组存储的过程和统一的类似对象名称的函数。|  
|序列|SSMA 创建序列对象 （SQL Server 2012 或 SQL Server 2014），或模拟 Oracle 序列。|  
|使用如索引和触发器的依赖对象的表|SSMA 使用从属对象创建表。|  
|触发器等依赖对象的视图|SSMA 创建包含依赖对象的视图。|  
|具体化的视图|**SSMA 使用一些例外情况创建 SQL server 上的索引的视图。如果实例化的视图包括一个或多个下列构造，转换将失败：**<br /><br />用户定义函数<br /><br />非确定性字段 / 函数 / 表达式在选择，其中或 GROUP BY 子句<br /><br />在选择 * Float 列用法其中或 GROUP BY 子句 （前面的问题的特殊用例）<br /><br />自定义数据类型 （包括嵌套表）<br /><br />计数 (非重复&lt;字段&gt;)<br /><br />FETCH<br /><br />OUTER 联接（LEFT、RIGHT 或 FULL）<br /><br />子查询，其他视图<br /><br />超过、 排名、 导致、 日志<br /><br />MIN、MAX<br /><br />UNION、 减号，相交<br /><br />HAVING|  
|触发器|**SSMA 创建触发器基于以下规则：**<br /><br />前触发器将转换为 INSTEAD of 触发器。<br /><br />AFTER 触发器将转换为 AFTER 触发器。<br /><br />INSTEAD OF 触发器将转换为 INSTEAD of 触发器。 在同一个操作上定义的多个 INSTEAD OF 触发器组合成一个触发器。<br /><br />行级触发器都被仿真的使用游标。<br /><br />级联触发器被转换为多个单独的触发器。|  
|同义词|**为下列对象类型创建同义词：**<br /><br />表和对象表<br /><br />视图和对象视图<br /><br />存储过程<br /><br />函数<br /><br />**解析并且直接对象引用替换为以下对象的同义词：**<br /><br />序列<br /><br />包<br /><br />Java 类架构对象<br /><br />用户定义的对象类型<br /><br />另一个同义词的同义词不能迁移，将标记为错误。<br /><br />同义词不 Materialized 视图的创建。|  
|用户定义的类型|**对于用户定义类型的转换，SSMA 不提供支持。用户定义类型，包括其用法 PL/SQL 程序中由以下规则指导的特殊转换错误标记：**<br /><br />表列的用户定义的类型转换为 varchar （8000）。<br /><br />自变量的用户定义的类型的存储过程或函数转换为 varchar （8000）。<br /><br />变量的 PL/SQL 块中的用户定义类型转换为 varchar （8000）。<br /><br />对象表转换为标准表。<br /><br />对象视图将转换为标准视图。|  
  
## <a name="converting-oracle-database-objects"></a>转换 Oracle 数据库对象  
若要转换 Oracle 数据库对象，你首先选择你想要转换的对象，然后执行转换的 SSMA。 若要查看输出消息在转换期间上,**视图**菜单上，选择**输出**。  
  
**若要将 Oracle 对象转换为 SQL Server 语法**  
  
1.  在 Oracle 元数据资源管理器中，展开在 Oracle 服务器，然后展开**架构**。  
  
2.  选择要转换的对象：  
  
    -   若要转换的所有架构，选中的复选框旁边**架构**。  
  
    -   若要将转换或省略数据库，选择架构名称旁边的复选框。  
  
    -   若要将转换或忽略的对象的类别，展开架构，然后选择或清除的类别旁边的复选框。  
  
    -   若要将转换或省略单个对象，展开类别文件夹中，然后选择或清除该对象旁边的复选框。  
  
3.  要将所有所选的对象的转换，请右键单击**架构**和选择**转换架构**。  
  
    您还可以通过右键单击该对象或其父文件夹，然后选择转换单个对象的类别**转换架构**。  
  
## <a name="viewing-conversion-problems"></a>查看转换问题  
某些 Oracle 对象可能不会转换。 你可以通过查看摘要转换报表来确定转换成功率。  
  
**若要查看摘要报表**  
  
1.  在 Oracle 元数据资源管理器中，选择**架构**。  
  
2.  在右窗格中，选择**报表**选项卡。  
  
    此报表显示所有数据库对象的已评估或转换摘要评估的报表。 你还可以查看摘要报表为单个对象：  
  
    -   若要查看的报表的单个架构，请在 Oracle 元数据资源管理器中选择的架构。  
  
    -   若要查看单个对象的报表，请在 Oracle 元数据资源管理器中选择的对象。 转换问题的对象具有红色错误图标。  
  
对于失败转换的对象，你可以查看导致转换失败的语法。  
  
**若要查看单个转换问题**  
  
1.  在 Oracle 元数据资源管理器中，展开**架构**。  
  
2.  展开显示红色错误图标的架构。  
  
3.  在架构中，展开具有红色错误图标的文件夹。  
  
4.  选择具有红色错误图标的对象。  
  
5.  在右窗格中，单击**报表**选项卡。  
  
6.  在顶部**报表**选项卡是下拉列表。 如果此列表显示**统计信息**，更改选定范围向**源**。  
  
    SSMA 显示的源代码和紧邻代码之上的多个按钮。  
  
7.  单击**下一步问题**按钮。 这是一个带有向右箭头的红色错误图标。  
  
    SSMA 将突出显示当前对象中找到的第一个有问题的源代码。  
  
对于无法转换每个项，您必须确定你想要使用该对象执行操作：  
  
-   你可以在修改过程的源代码**SQL**选项卡。  
  
-   你可以修改 Oracle 数据库可以删除或修改有问题的代码中的对象。 若要更新的代码载入 SSMA，你将需要更新的元数据。 有关详细信息，请参阅[连接到 Oracle 数据库 &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
-   你可以从迁移中排除对象。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器和 Oracle 元数据资源管理器中，在加载到对象之前清除项旁边的复选框[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和从 Oracle 的迁移数据。  
  
## <a name="next-step"></a>下一步  
迁移过程的下一步是[将已转换的对象加载到 SQL Server](http://msdn.microsoft.com/en-us/a8ae33b2-1883-4785-922b-ea0e31c0b37a)。  
  
## <a name="see-also"></a>另请参阅  
[将 Oracle 数据库迁移到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
