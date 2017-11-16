---
title: "数据库一致性检查 (DBCC) Analysis Services |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 28714c32-718f-4f31-a597-b3289b04b864
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2e8ecc3c51619c7f1ebbe5b109f0710500184a27
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="database-consistency-checker-dbcc-for-analysis-services"></a>Analysis Services 的数据库一致性检查 (DBCC)
  DBCC 为 Analysis Services 实例上的多维数据库和表格数据库提供按需数据库验证。 你可以在 SQL Server Management Studio (SSMS) 的 MDX 或 XMLA 查询窗口中执行 DBCC，并在 SQL Server Profiler 或 SSMS 的 xEvent 会话中跟踪 DBCC 输出。  
命令采用对象定义，如果对象已损坏，则返回空结果集或详细的错误信息。   在本文中，你将了解如何运行命令、解释结果以及解决出现的任何问题。  
  
 对于表格数据库，DBCC 执行的一致性检查相当于你每次加载、同步或还原数据库时自动进行的内置验证。  相比之下，对于多维数据库的一致性检查仅当你按需运行 DBCC 时才发生。  
  
 验证检查的范围根据模式的不同而异，表格数据库接受的检查范围更广。  
 DBCC 工作负载的特征也根据服务器模式的不同而异。 对多维数据库的检查操作包括从磁盘读取数据、构造要与实际索引进行比较的临时索引 - 所有这些操作花费的时间明显更长。  
  
 DBCC 的命令语法使用特定于所要检查数据库类型的对象元数据：  
  
-   多维和 SQL Server 2016 以前的表格 1100 或 1103 兼容级别数据库在 **cubeID**、 **measuregroupID**和 **partitionID**等多维建模构造中描述。  
  
-   元数据的兼容级别 1200年或更高版本的新表格模型数据库包含描述符喜欢**TableName**和**PartitionName**。  
  
 DBCC for Analysis Services 将在位于任何兼容级别的任何 Analysis Services 数据库上执行，前提是该数据库在 SQL Server 2016 实例上运行。 你只需确保为每个数据库类型使用正确的命令语法。  
  
> [!NOTE]  
>  如果熟悉 [DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)，很快就会发现 Analysis Services 中 DBCC 的作用域小地多。 Analysis Services 中的 DBCC 是单个命令，专门报告整个数据库或各个对象中的数据损坏。 如果你要考虑其他任务，例如收集信息，请尝试改用 AMO PowerShell 或 XMLA 脚本。 有关其他信息的链接，请参阅 [Monitor an Analysis Services Instance](../../analysis-services/instances/monitor-an-analysis-services-instance.md) 。  
  
## <a name="permission-requirements"></a>权限要求  
 你必须是 Analysis Services 数据库或服务器管理员（服务器角色的成员）才能运行该命令。 有关说明，请参阅[授予数据库权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) 或[向 Analysis Services 实例授予服务器管理员权限](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)。  
  
## <a name="command-syntax"></a>命令语法 
 在 1200年的表格数据库和更高版本的兼容性级别为对象定义中使用表格元数据。 以下示例演示了在 SQL Server 2016 功能级别创建的表格数据库的完整 DBCC 语法。  
  
 这两种语法之间的主要差异包括较新的 XMLA 命名空间，不\<对象 > 元素，但没有\<模型 > 元素 （没有每个数据库仍只能将一个模型）。  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2014/engine">  
     <DatabaseID>MyTabular1200DB_7811b5d8-c407-4203-8793-12e16c3d1b9b</DatabaseID>  
     <TableName>FactSales</TableName>  
     <PartitionName>FactSales 4</PartitionName>  
</DBCC>  
```  
  
 若要检查整个架构，可以省略较低级别的对象，例如表或分区名称。  
  
 可以在 Management Studio 中通过每个对象的属性页获取对象名称和 DatabaseID。  
  
## <a name="command-syntax-for-multidimensional-and-tabular-110x-databases"></a>适用于多维和表格 110x 数据库的命令语法  
 DBCC 为多维以及表格 1100 和 1103 数据库使用完全相同的语法。 你可以针对特定的数据库对象（包括整个数据库）运行 DBCC。 有关对象定义的详细信息，请参阅 [Object 元素 (XMLA)](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)。  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2006</PartitionID>  
     </Object>  
</DBCC>  
  
```  
  
 若要针对对象链中级别更高的对象运行 DBCC，请删除你不需要的任何较低级别对象 ID 元素：  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
     </Object>  
</DBCC>  
  
```  
  
 对于表格 110x 数据库，对象定义语法将在 Process 命令语法的后面建模（具体而言，涉及到如何将表映射到维度和度量值组）。  
  
-   **CubeID** 映射到模型 ID，即 **Model**。  
  
-   **MeasureGroupID** 映射到表 ID。  
  
-   **PartitionID** 映射到分区 ID。  
  
## <a name="usage"></a>用法  
 在 SQL Server Management Studio 中，你可以使用 MDX 或 XMLA 查询窗口调用 DBCC。 此外，你可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Profiler 或 Analysis Services xEvents 查看 DBCC 输出。 请注意，不会在 Windows 应用程序事件日志或 msmdsrv.log 文件中报告 SSAS DBCC 消息。  
  
 DBCC 将检查物理数据损坏，以及当段中存在孤立成员时发生的逻辑数据损坏。 在运行 DBCC 之前，必须先处理一个数据库。 DBCC 将跳过远程、空的或未处理的分区。  
  
 命令将在读取事务中运行，因此可能会被强制提交超时终止。 分区检查以并行方式运行。  
  
 拾取自上次重新启动服务以来发生的任何损坏错误时，可能需要重新启动服务。 重新连接到服务器不足以拾取这些更改。  
  
### <a name="run-dbcc-commands-in-management-studio"></a>在 Management Studio 中运行 DBCC 命令  
 若要运行即席查询，请在 SQL Server Management Studio 中打开一个 MDX 或 XMLA 查询窗口。 为此，请右键单击数据库 |“新建查询” | “XMLA”以运行命令并读取输出。  
  
 ![在 Management Studio 中的 DBCC XML 命令](../../analysis-services/instances/media/ssas-dbcc-ssms.gif "DBCC XML 在 Management Studio 中的命令")  
  
 如果未检测到任何问题，“结果”选项卡将指示一个空结果集（如屏幕截图中所示）。  
  
 “消息”选项卡提供详细信息，但这些信息对于小型数据库并一定总是正确。 状态消息有时会被修剪，指出命令已完成，但不提供针对每个对象的状态检查消息。 典型的消息报告看上去如下所示。  
  
 **DBCC 针对多维数据集验证检查报告的消息**  
  
```  
Executing the query ...  
READS, 0  
READ_KB, 0  
WRITES, 0  
WRITE_KB, 0  
CPU_TIME_MS, 0  
ROWS_SCANNED, 0  
ROWS_RETURNED, 0  
  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
<Object>  
<DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
<CubeID>Adventure Works</CubeID>  
</Object>  
</DBCC>  
Started checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2012' partition.  
Finished checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2013' partition.  
Finished checking segment indexes for the 'Internet_Sales_2012' partition.  
Started checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2011' partition.  
Finished checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2012' partition.  
Started checking segment indexes for the 'Internet_Orders_2013' partition.  
Finished checking segment indexes for the 'Internet_Orders_2012' partition.  
...   
Run complete  
  
```  
  
 **针对早期版本的 Analysis Services 运行 DBCC 后的输出**  
  
 只有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例上运行的数据库才支持 DBCC。 在较旧系统上运行该命令将返回此错误。  
  
```  
Executing the query ...  
The DBCC element at line 7, column 87 (namespace http://schemas.microsoft.com/analysisservices/2003/engine) cannot appear under Envelope/Body/Execute/Command.  
Execution complete  
  
```  
  
### <a name="trace-dbcc-output-in-sql-server-profiler-2016"></a>在 SQL Server Profiler 2016 中跟踪 DBCC 输出  
 可以在 Profiler 跟踪中查看 DBCC 输出，包括进度报告事件（进度报告开始、进度报告当前状态、进度报告结束和进度报告错误）。  
  
1.  启动跟踪。 有关如何在 Analysis Services 中使用 SQL Server Profiler 的帮助，请参阅 [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md) 。  
  
2.  选择“命令开始”和“命令结束”，以及任一或所有的“进度报告”事件。  
  
3.  使用上一部分提供的语法，在 Management Studio 的 XMLA 或 MDX 查询窗口中运行 DBCC 命令。  
  
4.  在 SQL Server Profiler 中，DBCC 活动是通过事件子类为 DBCC 的 **Command** 事件指示的：  
  
     ![ssas dbcc 探查器 eventsubclass](../../analysis-services/instances/media/ssas-dbcc-profiler-eventsubclass.PNG "ssas dbcc 探查器 eventsubclass")  
  
     事件代码 32 是 DBCC 执行。  
  
     事件代码 64 是针对单个对象的 DBCC 进度报告。  
  
     事件代码 63 是针对多维对象的段检查。  
  
     对于这两个事件子类，请查看 DBCC 返回的消息 **TextData** 值。  
  
     以开头的状态消息"的一致性检查\<对象 >"，"启动检查\<对象 >"，或"已检查完\<对象 >"。  
  
    > [!NOTE]  
    >  在 CTP 3.0 中，对象由内部名称标识。 例如，类别层次结构说明哪些情况下为 H$ 类别-\<objectID >。 在以后 CTP 中，内部名称应替换为用户友好的名称。  
  
     下面列出了错误消息。  
  
### <a name="trace-dbcc-output-in-an-xevent-session-in-ssms"></a>在 SSMS 的 xEvent 会话中跟踪 DBCC 输出  
 扩展的事件会话可以使用分析器事件或 xEvents。 有关添加 **Command** 和 **Progress Report** 事件的指导，请参阅上一部分。  
  
1.  通过右键单击数据库 >“管理” >“扩展事件” >  “会话” > “新建会话”来启动会话。 有关详细信息，请参阅  [Monitor Analysis Services with SQL Server Extended Events](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) 。  
  
2.  选择 Profiler 事件类别的任一或所有 **进度报告** 事件，或 PureXevent 类别的任一或所有 **RequestProgress** 事件。  
  
3.  使用上一部分提供的语法，在 Management Studio 的 XMLA 或 MDX 查询窗口中运行 DBCC 命令。  
  
4.  在 SSMS 中刷新“会话”文件夹。 右键单击会话名称 >“查看实时数据”。  
  
5.  查看 DBCC 为消息返回的 TextData 值。  TextData 是事件字段的属性，显示事件返回的状态和错误消息。  
  
     以开头的状态消息"的一致性检查\<对象 >"，"启动检查\<对象 >"，或"已检查完\<对象 >"。  
  
     下面列出了错误消息。  
  
## <a name="reference-consistency-checks-and-errors-for-multidimensional-databases"></a>参考：针对多维数据库的一致性检查和错误  
 对于多维数据库，只会验证分区索引。  在执行期间，DBCC 将为每个分区生成一个临时索引，并将该索引与磁盘上保留的索引进行比较。  生成临时索引需要从磁盘上的分区数据中读取所有数据，然后在内存中保存临时索引以供比较。 假设你有其他工作负载，你的服务器在运行 DBCC 执行时，可能会遇到磁盘 IO 和内存消耗较高的情况。  
  
 多维索引损坏检测包括以下检查。 发生对象级别的失败时，此表中的错误将出现在 xEvent 或 Profiler 跟踪中。  
  
||||  
|-|-|-|  
|**对象**|**DBCC 检查说明**|**失败时的错误**|  
|分区索引|检查段统计信息和索引。<br /><br /> 将临时分区索引中每个成员的 ID 与磁盘上存储的分区统计信息进行比较。  如果发现临时索引中某个成员的数据 ID 值超出了磁盘上为分区索引统计信息存储的范围，则将索引的统计信息视为已损坏。|分区段统计信息已损坏。|  
|分区索引|验证元数据。<br /><br /> 验证临时索引中的每个成员是否可以在磁盘上段的索引标头文件中找到。|分区段已损坏。|  
|分区索引|扫描段以查找物理损坏。<br /><br /> 在磁盘上的索引文件中读取临时索引中的每个成员，并验证索引记录的大小是否匹配，以及相同数据页是否标记为具有当前成员的记录。|分区段已损坏。|  
  
## <a name="reference-consistency-checks-and-errors-for-tabular-databases"></a>参考：针对表格数据库的一致性检查和错误  
 下表是针对表格对象执行的所有一致性检查列表，以及当检查指示损坏时引发的错误。 发生对象级别的失败时，此表中的错误将出现在 xEvent 或 Profiler 跟踪中。  
  
||||  
|-|-|-|  
|**对象**|**DBCC 检查说明**|**失败时的错误**|  
|数据库|检查数据库中的表计数。  值小于零表示损坏。|存储层有损坏。 “%{parent/}”数据库中的表集合损坏。|  
|数据库|检查用于跟踪引用完整性的内部结构，如果大小不正确则引发错误。|数据库文件无法通过一致性检查。|  
|表|检查用于确定表是维度表还是事实数据表的内部值。  如果值超出已知范围，则表示损坏。|检查表统计信息时数据库一致性检查 (DBCC) 失败。|  
|表|检查表段映射中的分区数是否与表的分区数匹配。|存储层有损坏。 “%{parent/}”表中的分区集合损坏。|  
|表|如果表格数据库是从 PowerPivot for Excel 2010 创建或导入的，并且分区计数大于 1，则将引发错误；随着分区支持添加到以后版本，将会指示损坏。|检查段映射时数据库一致性检查 (DBCC) 失败。|  
|分区|验证每个分区的数据段数以及每个段中数据段的记录数是否与段的索引中存储的值匹配。|检查段映射时数据库一致性检查 (DBCC) 失败。|  
|分区|如果总记录数、段数或每个段的记录数无效（小于零），或者段数不符合根据总记录数计算得出的所需段数，则引发错误。|检查段映射时数据库一致性检查 (DBCC) 失败。|  
|关系|如果用来存储有关关系的数据的结构不包含任何记录，或者在关系中使用的表名称为空，则引发错误。|检查关系时数据库一致性检查 (DBCC) 失败。|  
|关系|验证主表、主列、外表和外列的名称是否已设置，以及是否可访问关系所涉及的列和表。<br /><br /> 验证涉及的列类型是否有效，以及主键-外键值索引是否可生成有效的查找结构。|检查关系时数据库一致性检查 (DBCC) 失败。|  
|层次结构|如果层次结构的排序顺序不是识别的值，则引发错误。|检查层次结构“%{hier/}”时数据库一致性检查 (DBCC) 失败。|  
|层次结构|对层次结构执行的检查取决于使用的层次结构映射方案的内部类型。<br /><br /> 将检查所有层次结构的处理状态是否正确、层次结构存储是否存在，以及（如果适用）用于数据 ID 到层次结构位置转换的数据结构是否存在。<br /><br /> 假设通过了所有这些检查，将遍历层次结构以验证层次结构中的每个位置是否指向正确的成员。<br />如果其中的任何测试失败，则引发错误。|检查层次结构“%{hier/}”时数据库一致性检查 (DBCC) 失败。|  
|用户定义的层次结构|检查层次结构级别名称是否已设置。<br /><br /> 如果已处理层次结构，将检查内部层次结构数据存储的格式是否正确。  验证内部层次结构存储是否不包含任何无效的数据值。<br /><br /> 如果层次结构标记为未处理，则确认此状态是否适用于旧数据结构，并且层次结构的所有级别是否标记为空。|检查层次结构“%{hier/}”时数据库一致性检查 (DBCC) 失败。|  
|列|如果用于列的编码未设置为已知值，则引发错误。|检查列统计信息时数据库一致性检查 (DBCC) 失败。|  
|列|检查列是否已由内存中引擎压缩。|检查列统计信息时数据库一致性检查 (DBCC) 失败。|  
|列|检查列上的压缩类型是否为已知值。|检查列统计信息时数据库一致性检查 (DBCC) 失败。|  
|列|如果列“标记化”未设置为已知值，则引发错误。|检查列统计信息时数据库一致性检查 (DBCC) 失败。|  
|列|如果为列数据字典存储的 ID 范围与数据字典中的值数不匹配或者超出了允许的范围，则引发错误。|检查数据字典时数据库一致性检查 (DBCC) 失败。|  
|列|检查列的数据段数与它所属的表的数据段数是否匹配。|存储层有损坏。 “%{parent/}”列中的段集合已损坏。|  
|列|检查数据列的分区数是否与该列的数据段映射的分区数匹配。|检查段映射时数据库一致性检查 (DBCC) 失败。|  
|列|验证列段中的记录数是否与该列段的索引中存储的记录数匹配。|存储层有损坏。 “%{parent/}”列中的段集合已损坏。|  
|列|如果某个列没有段统计信息，则引发错误。|检查段统计信息时数据库一致性检查 (DBCC) 失败。|  
|列|如果某个列没有压缩信息或段存储，则引发错误。|数据库文件无法通过一致性检查。|  
|列|如果列的段统计信息不符合“最小数据 ID”、“最大数据 ID”的实际列值、非重复值数、行数或存在 NULL 值，则报告错误。|检查段统计信息时数据库一致性检查 (DBCC) 失败。|  
|ColumnSegment|如果最小数据 ID 或最大数据 ID 小于 NULL 的系统保留值，则将列段信息标记为已损坏。|检查段统计信息时数据库一致性检查 (DBCC) 失败。|  
|ColumnSegment|如果此段没有行，则应将列的最小和最大数据值设置为 NULL 的系统保留值。  如果值不为 null，则引发错误。|检查段统计信息时数据库一致性检查 (DBCC) 失败。|  
|ColumnSegment|如果列具有行和至少一个非 null 值，将检查列的最小和最大数据 ID 是否大于 NULL 的系统保留值。|检查段统计信息时数据库一致性检查 (DBCC) 失败。|  
|内部|验证是否已设置存储标记化提示、是否已处理存储，以及内部表是否存在有效指针。  如果未处理存储，则验证所有指针是否为 null。<br />否则，返回常规 DBCC 错误。|数据库文件无法通过一致性检查。|  
|DBCC 数据库|如果数据库架构中没有表，或者无法访问一个或多个表，则引发错误。|存储层有损坏。 “%{parent/}”数据库中的表集合损坏。|  
|DBCC 数据库|如果将表标记为临时或者具有未知类型，则引发错误。|遇到错误的表类型。|  
|DBCC 数据库|如果表的关系数为负值，或者为任一表定义了关系但找不到相应的关系结构，则引发错误。|存储层有损坏。 “%{parent/}”表中的关系集合损坏。|  
|DBCC 数据库|如果数据库的兼容级别为 1050 (SQL Server 2008 R2/PowerPivot v1.0) 并且关系数超出了模型中的表数，则将数据库标记为已损坏。|数据库文件无法通过一致性检查。|  
|DBCC 表|对于正在验证的表，检查列数是否小于零，如果为 true，则引发错误。  如果表中列的列存储为 NULL，则也会发生错误。|存储层有损坏。 “%{parent/}”表中的列集合损坏。|  
|DBCC 分区|检查正在验证的分区所属的表，如果表的列数小于零，则表示表的列集合已损坏。 如果表中列的列存储为 NULL，则也会发生错误。|存储层有损坏。 “%{parent/}”表中的列集合损坏。|  
|DBCC 分区|循环访问选定分区的每个列，并检查该分区的每个段是否与列段结构建立了有效链接。  如果任一段具有 NULL 链接，则将分区视为已损坏。|存储层有损坏。 “%{parent/}”列中的段集合已损坏。|  
|列|如果列类型无效，则返回错误。|遇到错误的段类型。|  
|列|如果任一列中的段数为负，或者指向段的列段结构的指针具有 NULL 链接，则返回错误。|存储层有损坏。 “%{parent/}”列中的段集合已损坏。|  
|DBCC 命令|DBCC 命令在处理 DBCC 操作过程中将报告多条状态消息。  在开始之前，它会报告包括数据库、表或对象列名的状态消息，在完成每个对象检查后再次报告一条消息。|检查一致性的\<objectname > \<objecttype >。 阶段: 前期检查。<br /><br /> 检查一致性的\<objectname > \<objecttype >。 阶段: 后期检查。|  
  
## <a name="common-resolutions-for-error-conditions"></a>错误状态的常见解决方法  
 SQL Server Management Studio 或 msmdsrv.log 文件中出现以下错误。 如果未通过一项或多项检查，将出现这些错误。 根据具体的错误，建议的解决方法是重新处理对象、删除并重新部署解决方案，或者还原数据库。  
  
|错误|问题|解决方法|  
|-----------|-----------|----------------|  
|**元数据管理器出错**<br /><br /> 对象引用\<objectID > 无效。 它与元数据类层次结构的结构不匹配。|命令格式不正确|检查命令语法。 很有可能你包含了一个较低级别的对象但未指定它的一个或多个父对象。|  
|**元数据管理器出错**<br /><br /> 任一\<对象 > id 为\<objectID > 中不存在\<parentobject > id 为\<parentobjectID >，或者用户没有权限访问该对象。|索引损坏（多维）|重新处理对象和所有依赖对象。|  
|**对分区执行一致性检查期间出错**<br /><br /> 检查的一致性时出错\<分区名称 > 的分区\<度量值组名称 > 的度量值组\<多维数据集名称 > 多维数据集来自\<数据库名称 > 数据库。 请重新处理分区或索引以修复损坏。|索引损坏（多维）|重新处理对象和所有依赖对象。|  
|**分区段统计信息损坏**|索引损坏（多维）|重新处理对象和所有依赖对象。|  
|**分区段损坏**|元数据损坏（多维或表格）|删除并重新部署项目，或者从备份还原，然后重新处理。<br /><br /> 有关说明，请参阅博客 [如何处理 Analysis Services 数据库中存在损坏](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) 。|  
|**表元数据损坏**<br /><br /> 表\<表名 > 元数据文件已损坏。 在 DataFileList 节点下找不到主表。|元数据损坏（仅限表格）|删除并重新部署项目，或者从备份还原，然后重新处理。<br /><br /> 有关说明，请参阅博客 [如何处理 Analysis Services 数据库中存在损坏](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) 。|  
|**存储层损坏**<br /><br /> 存储层损坏： 的集合\<类型名称 > 中\<父名称 >\<父类型 > 已损坏。|元数据损坏（仅限表格）|删除并重新部署项目，或者从备份还原，然后重新处理。<br /><br /> 有关说明，请参阅博客 [如何处理 Analysis Services 数据库中存在损坏](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) 。|  
|**缺少系统表**<br /><br /> 系统表\<表名 > 缺少。|对象损坏（仅限表格）|重新处理对象和所有依赖对象|  
|**表统计信息损坏**<br /><br /> 表系统表的统计信息\<表名 > 缺少。|元数据损坏（仅限表格）|删除并重新部署项目，或者从备份还原，然后重新处理。<br /><br /> 有关说明，请参阅博客 [如何处理 Analysis Services 数据库中存在损坏](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) 。|  
  
## <a name="disable-automatic-consistency-checks-on-database-load-operations-through--the-msmdsrvini-configuration-file"></a>通过 msmdsrv.ini 配置文件禁用对数据库加载操作的自动一致性检查  
 尽管不建议这样做，但你可以禁用自动对数据库加载事件进行的内置数据库一致性检查（仅限表格数据库）。 为此，需要在 msmdsrv.ini 文件中修改一项配置设置：  
  
```  
<ConfigurationSettings>  
     <Vertipaq />  
          <DisableConsistencyChecks />  
```  
  
 此设置在配置文件中不存在，你必须手动添加。  
  
 以下是有效值：  
  
-   **-2** （默认）已启用 DBCC。 如果服务器在逻辑上能够以较高的确定性解决错误，则自动应用修复程序。 否则，将记录错误。  
  
-   **-1** 已部分启用 DBCC。 已经为 RESTORE 启用，在事务结束时，将执行检查数据库状态的提交前验证。  
  
-   **0** 已部分启用 DBCC。 将在 RESTORE、IMAGELOAD、LOCALCUBELOAD 和 ATTACH 期间执行数据库一致性检查。  
         操作。  
  
-   **1** 已禁用 DBCC。 已禁用数据完整性检查，但反序列化检查仍会发生。  
  
> [!NOTE]  
>  按需运行命令时，此设置不影响 DBCC。  
  
## <a name="see-also"></a>另请参阅  
 [处理数据库、表或分区 (Analysis Services)](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)   
 [处理多维模型 (Analysis Services)](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [监视 Analysis Services 实例](../../analysis-services/instances/monitor-an-analysis-services-instance.md)   
 [Analysis Services 中表格模型的兼容级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)  
  
  

