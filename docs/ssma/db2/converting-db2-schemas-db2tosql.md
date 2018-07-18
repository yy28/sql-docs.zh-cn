---
title: 转换 DB2 架构 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
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
ms.assetid: 7947efc3-ca86-4ec5-87ce-7603059c75a0
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d6c63b66a52f0fbc6a676a2143299b7ee5b13208
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980699"
---
# <a name="converting-db2-schemas-db2tosql"></a>转换 DB2 架构 (DB2ToSQL)
已连接到 DB2 后，连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，并将项目设置和数据映射选项，可以将转换到 DB2 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库对象。  
  
## <a name="the-conversion-process"></a>转换过程  
将转换数据库对象从 DB2 所需的对象定义、 将其转换为类似[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象，再然后将此信息加载到 SSMA 元数据。 它不到的实例加载信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您然后可以通过查看对象和其属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器。  
  
在转换期间 SSMA 打印消息输出到输出窗格和错误消息为错误列表窗格。 使用的输出和错误的信息来确定是否必须修改您的 DB2 数据库或转换过程来获取所需的转换结果。  
  
## <a name="setting-conversion-options"></a>设置转换选项  
在将对象转换之前, 查看中的项目转换选项**项目设置**对话框。 通过使用此对话框中，可以设置 SSMA 将函数和全局变量的转换。 有关详细信息，请参阅[项目设置&#40;转换&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)。  
  
## <a name="conversion-results"></a>转换结果  
下表显示哪些 DB2 对象会转换与生成的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象：  
  
|DB2 对象|生成 SQL Server 对象|  
|-----------|----------------------------|  
|数据类型|**SSMA 映射除下面所列的下列每种类型：**<br /><br />CLOB： 与此类型的工作某些本机函数都不支持 (例如 CLOB_EMPTY())<br /><br />BLOB： 与此类型的工作某些本机函数都不支持 (例如 BLOB_EMPTY())<br /><br />DBLOB： 与此类型的工作某些本机函数都不支持 (例如 DBLOB_EMPTY())|  
|用户定义类型|**SSMA 映射以下用户：**<br /><br />不同的类型<br /><br />结构化的类型<br /><br />SQL PL 数据类型 – 请注意： 不支持弱游标类型。|  
|特殊寄存器|**SSMA 仅会在下面列出的寄存器：**<br /><br />当前时间戳<br /><br />当前日期<br /><br />当前时间<br /><br />当前时区<br /><br />当前用户<br /><br />SESSION_USER 和用户<br /><br />SYSTEM_USER<br /><br />当前 CLIENT_APPLNAME<br /><br />当前 CLIENT_WRKSTNNAME<br /><br />当前锁定超时<br /><br />当前架构<br /><br />当前服务器<br /><br />当前的隔离<br /><br />其他特殊的注册未映射到 SQL server 语义。|  
|CREATE TABLE|**SSMA 映射创建表，但存在以下例外：**<br /><br />多维聚类分析 (MDC) 表<br /><br />范围聚集表 (RCT)<br /><br />已分区的表<br /><br />已分离的表<br /><br />DATA CAPTURE 子句<br /><br />IMPLICITLY 隐藏选项<br /><br />易失性选项|  
|CREATE VIEW|SSMA 映射使用使用本地检查选项创建视图，但其他选项未映射到 SQL server 语义|  
|CREATE INDEX|**SSMA 映射创建索引，但存在以下例外：**<br /><br />XML 索引<br /><br />无需重叠 BUSINESS_TIME 选项<br /><br />已分区的子句<br /><br />仅规范选项<br /><br />使用扩展选项<br /><br />MINPCTUSED 选项<br /><br />页拆分选项|  
|触发器|**SSMA 会在以下触发器语义：**<br /><br />后/每行触发器<br /><br />每个语句后 /FOR 触发<br /><br />之前 / 对于每行，而不是 / 每行触发器|  
|序列|映射。|  
|SELECT 语句|**SSMA 映射选择有以下例外：**<br /><br />数据更改的表引用子句 – 部分映射，但最终表不受支持<br /><br />表引用子句 – 部分映射，但仅限表的引用、 外部表引用、 analyze_table 表达式集合派生表、 xmltable 表达式未映射到 SQL server 语义<br /><br />段规范子句 – 未映射。<br /><br />继续处理程序子句 – 未映射。<br /><br />类型化相关子句 – 未映射。<br /><br />并发访问解析子句 – 未映射。|  
|VALUES 语句|映射。|  
|INSERT 语句|映射。|  
|UPDATE 语句|S**SMA 映射更新具有以下例外：**<br /><br />表引用子句 – 仅限-表-引用未映射到 SQL server 语义<br /><br />时间段子句 – 未映射。|  
|MERGE 语句|**SSMA 将合并映射有以下例外：**<br /><br />单 vs 多个匹配项的每个子句-映射到 SQL server 语义，限制为出现的每个子句<br /><br />信号子句 – 不映射到 SQL Server 语义<br /><br />混合更新和删除子句 – 未映射到 SQL Server 语义<br /><br />段子句 – 不映射到 SQL Server 语义|  
|DELETE 语句|**SSMA 映射删除但存在以下例外：**<br /><br />表引用子句 – 仅限-表-引用未映射到 SQL server 语义<br /><br />时间段子句 – 不映射到 SQL Server 语义|  
|隔离级别和锁类型|映射。|  
|过程 (SQL)|映射。|  
|过程 （外部）|需要手动更新。|  
|过程 （来源）|不会映射到 SQL Server 语义。|  
|赋值语句|映射。|  
|有关过程的 CALL 语句|映射。|  
|CASE 语句|映射。|  
|FOR 语句|映射。|  
|GOTO 语句|映射。|  
|IF 语句|映射。|  
|迭代语句|映射。|  
|将语句|映射。|  
|循环语句|映射。|  
|重复执行语句|映射。|  
|语句重新发出通知|不支持条件。 消息可以是可选的。|  
|RETURN 语句|映射。|  
|信号语句|不支持条件。 消息可以是可选的。|  
|WHILE 语句|映射。|  
|获取诊断语句|**SSMA 会获取诊断有以下例外：**<br /><br />映射 ROW_COUNT –。<br /><br />映射 DB2_RETURN_STATUS –。<br /><br />映射 MESSAGE_TEXT –。<br /><br />DB2_SQL_NESTING_LEVEL-不映射到 SQL Server 语义<br /><br />DB2_TOKEN_STRING-不映射到 SQL Server 语义|  
|游标|**SSMA 将游标映射有以下例外：**<br /><br />分配游标语句-不映射到 SQL Server 语义<br /><br />将关联的定位符语句-不映射到 SQL Server 语义<br /><br />DECLARE CURSOR 语句-Returnability 子句未映射到 SQL server 语义<br /><br />FETCH 语句 – 部分映射。 仅支持作为目标的变量。 SQLDA 描述符未映射到 SQL server 语义|  
|变量|映射。|  
|异常、 处理程序和条件|**SSMA 映射"异常处理"，但存在以下例外：**<br /><br />退出处理程序 – 映射。<br /><br />撤消处理程序 – 映射。<br /><br />继续处理程序 – 未映射。<br /><br />条件-它不映射到 SQL server 语义。|  
|动态 SQL|未映射。|  
|Aliases|映射。|  
|昵称|部分映射。 所需的基础对象的手动处理|  
|同义词|映射。|  
|在 DB2 中的标准函数|SSMA 映射 DB2 标准函数等功能在 SQL Server 中不可用：|  
|授权|未映射。|  
|谓词|映射。|  
|SELECT INTO 语句|未映射。|  
|值 INTO 语句|未映射。|  
|控制事务|未映射。|  
  
## <a name="converting-db2-database-objects"></a>转换 DB2 数据库对象  
将 DB2 数据库对象时，您首先选择你想要转换的对象，然后执行转换的 SSMA。 若要在转换期间查看输出消息上**视图**菜单中，选择**输出**。  
  
**若要将 DB2 对象转换为 SQL Server 语法**  
  
1.  在 DB2 元数据资源管理器中，展开 DB2 服务器，然后展开**架构**。  
  
2.  选择要转换的对象：  
  
    -   若要将所有架构，选择复选框旁边**架构**。  
  
    -   若要将转换或省略数据库，选择架构名称旁边的复选框。  
  
    -   若要将转换或忽略的对象的类别，展开架构，然后选择或清除类别旁边的复选框。  
  
    -   若要将转换或忽略各个对象，展开类别文件夹，然后选择或清除的对象旁边的复选框。  
  
3.  若要将所有选定的对象的转换，请右键单击**架构**，然后选择**转换架构**。  
  
    您还可以通过右键单击该对象或其父文件夹，然后选择转换单个对象的类别**转换架构**。  
  
## <a name="viewing-conversion-problems"></a>查看转换问题  
DB2 的某些对象可能不会转换。 您可以查看摘要转换报告来确定转换成功率。  
  
**若要查看摘要报表**  
  
1.  在 DB2 元数据资源管理器中，选择**架构**。  
  
2.  在右窗格中，选择**报表**选项卡。  
  
    此报表显示所有数据库对象的已评估或转换摘要评估的报表。 你还可以查看摘要报告为单个对象：  
  
    -   若要查看单个架构的报表，在 DB2 元数据资源管理器中选择的架构。  
  
    -   若要查看单个对象的报表，请在 DB2 元数据资源管理器中选择的对象。 具有转换问题的对象都有红色错误图标。  
  
对于无法转换的对象，可以查看导致转换失败的语法。  
  
**若要查看单个转换问题**  
  
1.  在 DB2 元数据资源管理器中，展开**架构**。  
  
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
  
-   可以修改要删除或修改有问题的代码的 DB2 数据库中的对象。 若要将更新的代码加载到 SSMA，必须更新元数据。 有关详细信息，请参阅[连接到 DB2 数据库&#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)。  
  
-   您可以从迁移中排除对象。 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器和 DB2 的元数据资源管理器中，加载到对象之前清除项旁边的复选框[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和将数据从 DB2 迁移。  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是[加载到 SQL Server 的已转换的对象](http://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3)。  
  
## <a name="see-also"></a>请参阅  
[将 DB2 数据迁移到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
