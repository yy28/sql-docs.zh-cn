---
title: 转换 Oracle 架构 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Conversion Results
ms.assetid: e021182d-31da-443d-b110-937f5db27272
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 18da150a435b5d3d61740139309d109a16691da3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788505"
---
# <a name="converting-oracle-schemas-oracletosql"></a>转换 Oracle 架构 (OracleToSQL)
已连接到 Oracle 后，连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，并将项目设置和数据映射选项，可以将转换到的 Oracle 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库对象。  
  
## <a name="the-conversion-process"></a>转换过程  
将转换数据库对象从 Oracle 获取的对象定义、 将其转换为类似[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对象，再然后将此信息加载到 SSMA 元数据。 它不到的实例加载信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您然后可以通过查看对象和其属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器。  
  
在转换期间 SSMA 打印消息输出到输出窗格和错误消息为错误列表窗格。 使用的输出和错误的信息来确定是否必须修改您的 Oracle 数据库或转换过程来获取所需的转换结果。  
  
## <a name="setting-conversion-options"></a>设置转换选项  
在将对象转换之前, 查看中的项目转换选项**项目设置**对话框。 通过使用此对话框中，可以设置 SSMA 将函数和全局变量的转换。 有关详细信息，请参阅[项目设置&#40;转换&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)。  
  
## <a name="conversion-results"></a>转换结果  
下表显示了哪些 Oracle 对象会转换与生成的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对象：  
  
|||  
|-|-|  
|Oracle 对象|生成 SQL Server 对象|  
|函数|如果该函数可直接转换为[!INCLUDE[tsql](../../includes/tsql-md.md)]，SSMA 创建一个函数。<br /><br />在某些情况下，该函数必须转换为存储过程。 在这种情况下，SSMA 创建存储的过程和调用存储的过程的函数。|  
|过程|如果该过程可以直接转换为[!INCLUDE[tsql](../../includes/tsql-md.md)]，SSMA 创建的存储的过程。<br /><br />在某些情况下必须自治事务中调用存储的过程。 SSMA 在这种情况下，创建两个存储的过程： 一个实现过程，以及用来调用实现的另一个存储过程。|  
|包|SSMA 创建一组存储的过程和统一的类似对象名称的函数。|  
|序列|SSMA 创建序列对象 （SQL Server 2012 或 SQL Server 2014），或模拟 Oracle 序列。|  
|具有依赖对象，如索引和触发器的表|SSMA 创建包含依赖对象的表。|  
|查看与依赖对象，如触发器|SSMA 创建包含依赖对象的视图。|  
|具体化的视图|**SSMA 有一些例外情况创建 SQL server 上的索引的视图。如果实例化的视图包含一个或多个以下的构造，转换将失败：**<br /><br />用户定义函数<br /><br />非确定性的字段 / 函数 / 表达式在中，选择其中或 GROUP BY 子句<br /><br />Float 列中选择 * 的用法，或 GROUP BY 子句 （上一个问题的特殊情况下）<br /><br />自定义数据类型 （包括嵌套表）<br /><br />COUNT (distinct&lt;字段&gt;)<br /><br />FETCH<br /><br />OUTER 联接（LEFT、RIGHT 或 FULL）<br /><br />子查询，其他视图<br /><br />超过、 排名、 导致日志<br /><br />MIN、MAX<br /><br />UNION、 减号，INTERSECT<br /><br />HAVING|  
|触发器|**SSMA 创建触发器根据以下规则：**<br /><br />前触发器将转换为 INSTEAD of 触发器。<br /><br />AFTER 触发器将转换为 AFTER 触发器。<br /><br />INSTEAD OF 触发器将转换为 INSTEAD of 触发器。 多个相同的操作上定义的 INSTEAD OF 触发器被结合到一个触发器。<br /><br />行级触发器都被仿真使用游标。<br /><br />级联触发器将转换为多个单个触发器。|  
|同义词|**为以下对象类型创建同义词：**<br /><br />表和对象表<br /><br />视图和对象视图<br /><br />存储过程<br /><br />函数<br /><br />**解析并直接对象的引用替换为以下对象的同义词：**<br /><br />序列<br /><br />包<br /><br />Java 类架构对象<br /><br />用户定义的对象类型<br /><br />另一个同义词的同义词不能迁移，并将标记为错误。<br /><br />同义词不会为 Materialized 视图创建。|  
|用户定义的类型|**SSMA 不为用户定义类型的转换提供支持。用户定义类型，PL/SQL 程序中包括其使用情况将标有特殊转换错误由以下规则：**<br /><br />表列的用户定义的类型转换为 VARCHAR(8000)。<br /><br />自变量的用户定义类型到存储过程或函数转换为 VARCHAR(8000)。<br /><br />PL/SQL 块中的用户定义类型的变量转换为 VARCHAR(8000)。<br /><br />对象表转换为标准表。<br /><br />对象视图转换为标准视图。|  
  
## <a name="converting-oracle-database-objects"></a>转换 Oracle 数据库对象  
将 Oracle 数据库对象时，您首先选择你想要转换的对象，然后执行转换的 SSMA。 若要在转换期间查看输出消息上**视图**菜单中，选择**输出**。  
  
**若要将 Oracle 对象转换为 SQL Server 语法**  
  
1.  在 Oracle 元数据资源管理器中，展开 Oracle 服务器，然后展开**架构**。  
  
2.  选择要转换的对象：  
  
    -   若要将所有架构，选择复选框旁边**架构**。  
  
    -   若要将转换或省略数据库，选择架构名称旁边的复选框。  
  
    -   若要将转换或忽略的对象的类别，展开架构，然后选择或清除类别旁边的复选框。  
  
    -   若要将转换或忽略各个对象，展开类别文件夹，然后选择或清除的对象旁边的复选框。  
  
3.  若要将所有选定的对象的转换，请右键单击**架构**，然后选择**转换架构**。  
  
    您还可以通过右键单击该对象或其父文件夹，然后选择转换单个对象的类别**转换架构**。  
  
## <a name="viewing-conversion-problems"></a>查看转换问题  
可能不会转换某些 Oracle 对象。 您可以查看摘要转换报告来确定转换成功率。  
  
**若要查看摘要报表**  
  
1.  在 Oracle 元数据资源管理器中，选择**架构**。  
  
2.  在右窗格中，选择**报表**选项卡。  
  
    此报表显示所有数据库对象的已评估或转换摘要评估的报表。 你还可以查看摘要报告为单个对象：  
  
    -   若要查看单个架构的报表，请在 Oracle 元数据资源管理器选择的架构。  
  
    -   若要查看单个对象的报表，请在 Oracle 元数据资源管理器中选择的对象。 具有转换问题的对象都有红色错误图标。  
  
对于无法转换的对象，可以查看导致转换失败的语法。  
  
**若要查看单个转换问题**  
  
1.  在 Oracle 元数据资源管理器中，展开**架构**。  
  
2.  展开显示红色错误图标的架构。  
  
3.  在架构中，展开具有红色错误图标的文件夹。  
  
4.  选择具有红色错误图标的对象。  
  
5.  在右窗格中，单击**报表**选项卡。  
  
6.  在顶部**报表**选项卡是一个下拉列表。 如果列表中显示**统计信息**，更改到所选**源**。  
  
    SSMA 显示的源代码和几个按钮，上面的代码。  
  
7.  单击**下一个问题**按钮。 这是一个红色错误图标的向右箭头。  
  
    SSMA 将突出显示第一个有问题的源代码的当前对象中找到。  
  
对于无法转换每个项，您需要确定想要使用该对象执行操作：  
  
-   可以在修改过程的源代码**SQL**选项卡。  
  
-   可以修改要删除或修改有问题的代码的 Oracle 数据库中的对象。 若要将更新的代码加载到 SSMA，必须更新元数据。 有关详细信息，请参阅[连接到 Oracle 数据库&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
-   您可以从迁移中排除对象。 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器和 Oracle 元数据资源管理器中，加载到对象之前清除项旁边的复选框[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和将数据从 Oracle 迁移。  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是[加载到 SQL Server 的已转换的对象](loading-converted-database-objects-into-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>请参阅  
[迁移的 Oracle 数据库移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
