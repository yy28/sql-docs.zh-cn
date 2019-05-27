---
title: SQL Server Management Studio 中使用 Analysis Services 模板 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 54ad1954-22e2-4628-b334-8fad8e9433b8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca2f92441841168916cb3d50b63376634073456b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079547"
---
# <a name="use-analysis-services-templates-in-sql-server-management-studio"></a>Use Analysis Services Templates in SQL Server Management Studio
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供一组模板来帮助您快速创建 XMLA 脚本、DMX 或 MDX 查询，在多维数据集或表格模型中创建 KPI，执行脚本备份和还原操作，以及执行其他许多任务。 模板位于 **的** “模板资源管理器” [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中。  
  
 本主题包括多维模型和表格模型的模板列表，并且提供如何通过使用元数据资源管理器和模板资源管理器生成 MDX 查询和 XMLA 语句的示例。  
  
 本主题包含以下各节：  
  
 [打开 Analysis Services 模板](#bkmk_usingTE)  
  
 [使用模板对表格模型生成并运行 MDX 查询](#BKMK_Building_Queries)  
  
 [从模板创建 XMLA 脚本](#bkmk_backup)  
  
 [使用 XMLA 模板生成架构行集查询](#bkmk_schemarowset)  
  
 [Analysis Services 模板参考](#bkmk_Ref)  
  
 本主题不涉及 DMX 模板。 有关如何使用模板创建数据挖掘查询的示例，请参阅 [在 SQL Server Management Studio 中创建一个 DMX 查询](../data-mining/create-a-dmx-query-in-sql-server-management-studio.md) 或 [通过模板创建单独预测查询](../data-mining/create-a-singleton-prediction-query-from-a-template.md)。  
  
##  <a name="bkmk_usingTE"></a> 打开 Analysis Services 模板  
 用于数据库引擎查询以及 Analysis Services 查询和命令的所有模板均在模板资源管理器中提供。  
  
 若要打开 **“模板资源管理器”**，请从 **“视图”** 菜单中选择它。 接下来，单击多维数据集图标可以查看可用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的模板的列表。  
  
 ![为 Analysis Services 模板资源管理器，筛选](../media/ssas-templateexplorer.gif "模板资源管理器，筛选出的 Analysis Services")  
  
 若要打开某一模板，请右键单击该模板名称，然后选择“打开”，或者将模板拖到已经打开的查询窗口中。 在查询窗口打开后，您可以使用工具栏或“查询”菜单上的命令来帮助您生成语句：  
  
-   若要查看查询的语法，请单击 **“分析”**。  
  
-   若要运行查询，请单击 **“执行”**。  
  
     若要停止正在运行的查询，请单击 **“取消执行查询”**。  
  
-   在屏幕底部的 **“结果”** 选项卡中查看查询的结果。  
  
     切换到 **“消息”** 选项卡可以查看返回的记录数以及与查询执行相关联的错误、查询语句和任何其他消息。 例如，如果您对在直接查询模式下运行的模型执行 DAX 语句，则可以看到由 xVelocity 内存中分析引擎 (VertiPaq) 生成的 Transact-SQL 语句。  
  
##  <a name="BKMK_Building_Queries"></a> 使用模板对表格模型生成并运行 MDX 查询  
 此实例说明如何在 SQL Server Management Studio 中创建 MDX 查询，并且使用表格模型数据库作为数据源。 若要在您的计算机上重复此示例，您可以 [下载 Adventureworks 表格模型示例项目](https://go.microsoft.com/fwlink/?LinkId=231183)。  
  
> [!WARNING]  
>  不能对已在直接查询模式下部署的表格模型使用 MDX 查询。 但是，可以通过将 DAX 表查询用于 EVALUATE 命令来发送等效的查询。 有关详细信息，请参阅[DAX 查询的参数](https://msdn.microsoft.com/library/gg492200(v=sql.120).aspx)。  
  
#### <a name="create-an-mdx-query-from-a-template"></a>从模板创建 MDX 查询  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开包含要查询的表格模型的实例。 右键单击数据库图标，选择“新建查询”，然后选择“MDX”。  
  
2.  在模板浏览器的 Analysis Services 模板中，打开 **MDX**，然后打开 **“查询”**。 将 **“基本查询”** 拖到查询窗口。  
  
3.  使用 **“元数据资源管理器”**，将下列字段和度量值拖到查询模板：  
  
    1.  替换\<row_axis，mdx_set > 与 **[Product Category]。 [产品类别名称]**。  
  
    2.  替换\<column_axis，mdx_set > 与 **[Date]。 [日历年]。[Calendar Year]**.  
  
    3.  替换\<from_clause，mdx_name > 与 **[Internet 销售额]**。  
  
    4.  替换\<where_clause，mdx_set > 与 **[Measures]。 [Internet 总销售额]**。  
  
4.  您可以按原样执行此查询，但您可能会想要进行某些更改，例如添加函数以便返回特定成员。 例如，键入`.members`后 **[Product Category]。 [产品类别名称]**。 有关详细信息，请参阅 [Using Member Expressions](/sql/mdx/using-member-expressions)。  
  
##  <a name="bkmk_backup"></a> 从模板创建 XMLA 脚本  
 在模板资源管理器中提供的 XMLA 命令模板可用于为监视和更新 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象创建脚本，而与实例是处于多维和数据挖掘模式下还是表格模式下无关。 **XMLA** 模板包含针对下列类型的脚本的示例：  
  
-   备份、还原和同步操作  
  
-   取消指定的进程或命令  
  
-   处理对象  
  
-   发现架构行集  
  
-   监视服务器状态，包括作业、连接、事务、内存和性能计数器  
  
#### <a name="create-a-backup-command-script-from-a-template"></a>从模板创建备份命令脚本  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开包含要查询的数据库的实例。 右键单击数据库图标，选择“新建查询”，然后选择“XMLA”。  
  
    > [!WARNING]  
    >  您不能通过更改限制列表或通过在连接对话框中指定数据库来设置 XMLA 查询的上下文。 您必须从要查询的数据库打开 XMLA 查询窗口。  
  
2.  拖动`Backup`到空查询窗口中的模板。  
  
3.  双击中的文本\<DatabaseID > 元素。  
  
4.  在对象资源管理器中，选择要备份的数据库，然后将该数据库拖放到 DatabaseID 元素的括号之间。  
  
5.  双击中的文本\<文件 > 元素。 键入备份文件的名称，包括 .abf 文件扩展名。 如果您不使用默认的备份位置，则指定完整的文件路径。 有关详细信息，请参阅[备份、还原和同步数据库 (XMLA)](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
##  <a name="bkmk_schemarowset"></a> 使用 XMLA 模板生成架构行集查询  
 **“模板资源管理器”** 对于架构行集查询仅包含一个模板。 若要使用此模板，您必须熟悉要使用的单独架构行集的要求，并且包含所需所有元素以及可用作限制的列。 有关详细信息，请参阅 [Analysis Services 架构行集](https://docs.microsoft.com/bi-reference/schema-rowsets/analysis-services-schema-rowsets)。  
  
 请注意，出于简便目的，许多架构行集也作为动态管理视图 (DMV) 公开。 通过使用相应的 DMV，您可以使用与 Transact-SQL 相似的语法来查询架构行集。 例如，下面的查询返回相同的结果，但一个查询以 XML 格式返回结果，而另一个查询以表格格式返回结果。 有关 DMV 的详细信息，请参阅[使用动态管理视图 (DMV) 监视 Analysis Services](use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)。  
  
 返回可用作 DMV 的所有架构行集的列表的 DMV：  
  
```  
SELECT * FROM $system.DISCOVER_SCHEMA_ROWSETS  
```  
  
 返回可用架构行集的列表的 XMLA 命令：  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
<RequestType>DISCOVER_SCHEMA_ROWSETS</RequestType>  
    <Restrictions>  
<RestrictionList>  
</RestrictionList>  
</Restrictions>  
    <Properties>  
<PropertyList>  
   </PropertyList>  
</Properties>  
</Discover>  
```  
  
#### <a name="get-a-list-of-data-sources-for-a-tabular-model-using-a-schema-rowset-query"></a>使用架构行集查询获取表格模型的数据源的列表  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开包含要查询的数据库的实例。 右键单击数据库图标，选择“新建查询”，然后选择“XMLA”。  
  
    > [!WARNING]  
    >  您不能通过更改限制列表或通过在连接对话框中指定数据库来设置 XMLA 查询的上下文。 您必须从要查询的数据库打开 XMLA 查询窗口。  
  
2.  打开 **“模板资源管理器”**，将模板 **“发现架构行集”** 拖入空白查询窗口中。  
  
3.  在模板中，替换[RequestType 元素&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla)元素具有以下文本： `<RequestType>MDSCHEMA_INPUT_DATASOURCES</RequestType>`  
  
4.  单击 **“执行”**。  
  
     预期的结果：  
  
    ```  
    <CATALOG_NAME>AW Internet Sales Tabular Model_ 24715b71-ea74-4828-aefc-d4c12c15db64</CATALOG_NAME>   
    <DATASOURCE_NAME>SqlServer localhost AdventureWorksDW2012</DATASOURCE_NAME>   
    <DATASOURCE_TYPE>Relational</DATASOURCE_TYPE>   
    <CREATED_ON>2011-10-12T20:27:05.196667</CREATED_ON>   
    <LAST_SCHEMA_UPDATE>2011-10-12T20:27:05.196667</LAST_SCHEMA_UPDATE>   
    <DESCRIPTION />   
    <TIMEOUT>0</TIMEOUT>   
    <DBMS_NAME>Microsoft SQL Server</DBMS_NAME>   
    <DBMS_VERSION>11.00.1724</DBMS_VERSION>  
  
    ```  
  
##  <a name="bkmk_Ref"></a> Analysis Services 模板参考  
 提供以下模板以便使用 Analysis Services 数据库以及数据库中的对象，包括挖掘结构和挖掘模型、多维数据集和表格模型：  
  
|Category|项模板|Description|  
|--------------|-------------------|-----------------|  
|DMX\模型内容|内容查询|演示如何使用 DMX SELECT FROM *\<模型 >*。内容语句，检索指定的挖掘模型的挖掘模型架构行集内容。|  
||连续列值|演示如何使用 DMX SELECT DISTINCT FROM *\<模型 >* 语句与 DMX`RangeMin`和`RangeMax`函数来从中的连续列检索指定范围内的值的一组指定的挖掘模型。|  
||离散列值|演示如何使用 DMX SELECT DISTINCT FROM *\<模型 >* 语句从指定的挖掘模型中的离散列检索一组完整的值。|  
||钻取查询|演示如何将 DMX SELECT * FROM Model.CASES 语句与 DMX IsInNode 函数一起使用来执行钻取查询|  
||模型属性|演示如何使用 DMX System.GetModelAttributes 函数返回模型所用属性的列表。|  
||PMML 内容|演示如何使用 DMX SELECT \* FROM *\<模型 >*。PMML 语句检索挖掘模型，适用于支持此功能的算法的预测模型标记语言 (PMML) 表示形式。|  
|DMX\模型管理|添加模型|演示如何使用 DMX ALTER MINING MODEL STRUCTURE 语句添加挖掘模型|  
||清除模型|演示如何使用 DMX DELETE * FROM MINING MODEL 语句删除指定挖掘模型的内容。|  
||清除结构事例|演示如何使用 DMX DELETE FROM MINING STRUCTURE 语句清除挖掘模型结构事例|  
||清除结构|演示如何使用 DMX DELETE FROM MINING STRUCTURE 语句清除挖掘模型结构|  
||从 PMML 创建|演示如何将 DMX CREATE MINING MODEL 语句与 FROM PMML 子句一起使用来从 PMML 表示创建挖掘模型。|  
||创建嵌套结构|演示如何将 DMX CREATE MINING STRUCTURE 语句与嵌套列定义列表一起使用来创建带有嵌套列的挖掘模型。|  
||创建结构|演示如何使用 DMX CREATE MINING STRUCTURE 语句创建挖掘模型。|  
||删除模型|演示如何使用 DMX DROP MINING MODEL 语句删除现有挖掘模型。|  
||删除结构|演示如何使用 DMX DROP MINING STRUCTURE 语句删除现有挖掘结构。|  
||导出模型|演示如何使用带有 WITH DEPENDENCIES 子句和 PASSWORD 子句的 DMX EXPORT MINING MODEL 语句将挖掘模型（包括该挖掘模型所基于的数据源和数据源视图）导出到文件。|  
||导出结构|演示如何使用带有 WITH DEPENDENCIES 子句的 DMX EXPORT MINING STRUCTURE 语句将挖掘结构（包括该挖掘结构所包含的所有挖掘模型与该挖掘结构所基于的数据源和数据源视图）导出到文件。|  
||导入|展示了如何结合使用 DMX IMPORT FROM 语句和 WITH PASSWORD 子句来执行导入。|  
||重命名模型|演示如何使用 DMX RENAME MINING MODEL 语句重命名现有挖掘模型。|  
||重命名结构|演示如何使用 DMX RENAME MINING STRUCTRE 语句重命名现有挖掘结构。|  
||定型模型|演示如何使用 DMX INSERT INTO MINING MODEL 语句在先前定型的结构内部定型挖掘模型。|  
||定型嵌套结构|演示如何将 DMX INSERT INTO MINING STRUCTURE 语句和 SHAPE 源数据查询组合使用来定型这样的挖掘模型，该挖掘模型包含嵌套列，而嵌套列中的数据包含使用查询从现有数据源检索到的嵌套表。|  
||定型结构|演示如何将 DMX INSERT INTO MINING STRUCTURE 语句和 OPENQUERY 源数据查询组合使用来定型挖掘结构。|  
|DMX\预测查询|基准预测|演示如何组合使用 DMX SELECT FROM *\<模型 >* PREDICTION JOIN 语句和 OPENQUERY 源数据查询来执行针对使用数据，使用一个查询，从检索到的挖掘模型的预测查询现有数据源。|  
||嵌套预测|演示如何组合使用 DMX SELECT FROM *\<模型 >* PREDICTION JOIN 语句与 SHAPE 和 OPENQUERY 源数据查询来执行针对使用包含嵌套的数据的挖掘模型的预测查询使用查询从现有数据源检索到的表。|  
||嵌套单独预测|演示如何使用 DMX SELECT FROM *\<模型 >* NATURAL PREDICTION JOIN 子句，以执行针对使用单个值，在中列的预测查询中显式指定的挖掘模型的预测查询其名称与挖掘模型中的列，其中包含一组值中使用名称也匹配到挖掘模型中的嵌套列的 UNION 语句创建的嵌套表。|  
||单独预测|演示如何使用 DMX SELECT FROM 使用\<模型 > NATURAL PREDICTION JOIN 语句来执行针对使用单个值，在中其名称与中的列的列的预测查询中显式指定的挖掘模型的预测查询挖掘模型。|  
||存储过程调用|演示如何使用 DMX CALL 语句调用存储过程|  
|MDX\表达式|变动平均值 - 固定|演示如何使用 MDX `ParallelPeriod` 和 `CurrentMember` 函数及自然排序集生成一个计算度量值，以便提供一个度量值在时间维度的一个层次结构所包含的一个固定数量时间段上的变动平均值。|  
||变动平均值 - 可变|演示如何在 `CASE` 函数内使用 MDX `Avg` 语句来生成一个计算度量值，以便提供一个度量值在时间维度的一个层次结构所包含的一个可变数量时间段上的变动平均值。|  
||本期截止到现在|演示如何在计算成员内使用 MDX `PeriodsToDate` 函数。|  
||父级比率|演示如何使用 MDX `Parent` 函数来创建一个计算度量值，以便表示指定层次结构中父成员的每个子成员的度量值的百分率。|  
||总计比率|演示如何使用“全部”成员来创建一个计算度量值，以便表示指定层次结构中每个成员的度量值的百分率。|  
|MDX\查询|“基本查询”|演示一个可从其构造 MDX 查询的基本 MDX SELECT 语句。|  
||KPI 查询|演示如何在 MDX 查询中使用 MDX `KPIValue` 和 `KPIGoal` 函数来检索关键绩效指标 (KPI) 信息。|  
||嵌套 Select 查询|演示如何创建一个从由另一个 SELECT 语句定义的子多维数据集中检索信息的 MDX SELECT 语句。|  
||使用计算成员|演示如何在 SELECT 语句中使用 MDX WITH 子句来为 MDX 查询定义计算成员。|  
||使用命名集|演示如何在 SELECT 语句中使用 MDX WITH 子句来为 MDX 查询定义命名集。|  
|XMLA\管理|Backup|演示如何使用 XMLA `Backup` 命令将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库备份到文件。|  
||取消|演示如何使用 XMLA `Cancel` 命令取消针对当前会话（用于用户而不是管理员或服务器管理员）、数据库（用于管理员）或实例（用于服务器管理员）运行的所有操作。|  
||创建远程分区数据库|演示如何使用 XMLA `Create` 命令和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 数据库元素来创建用于存储远程分区的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库和数据源。|  
||DELETE|演示如何使用 XMLA `Delete` 命令删除现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。|  
||处理维度|演示如何将 XMLA `Batch` 命令与 `Parallel` 元素和 `Process` 命令组合使用来通过使用并行批处理操作更新维度的属性。|  
||处理分区|演示如何将 XMLA `Batch` 命令与 `Parallel` 元素和 `Process` 命令组合使用来通过并行批处理操作完全处理一个分区。|  
||还原|演示如何使用 XMLA `Restore` 命令从现有备份文件还原 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。|  
||同步|演示如何使用 XMLA `Synchronize` 命令，并针对 SynchronizeSecurity 标记使用 SkipMembership 选项，将另一个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库与当前 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库进行同步。|  
|XMLA\架构行集|发现架构行集|演示如何使用 XMLA `Discover` 方法检索 DISCOVER_SCHEMA_ROWSETS 架构行集的内容。|  
|XMLA\服务器状态|连接|演示如何使用 XMLA `Discover` 方法检索 DISCOVER_CONNECTIONS 架构行集的内容。|  
||中执行计划的管理任务，即“作业”|演示如何使用 XMLA `Discover` 方法检索 DISCOVER_JOBS 架构行集的内容。|  
||位置|演示如何使用 XMLA `Discover` 方法并指定位置备份文件的路径来检索 DISCOVER_LOCATIONS 架构行集的内容。|  
||锁|演示如何使用 XMLA `Discover` 方法检索 DISCOVER_LOCKS 架构行集的内容。|  
||内存授予|演示如何使用 XMLA `Discover` 方法检索 DISCOVER_MEMORYGRANT 架构行集的内容。|  
||性能计数器|演示如何使用 XMLA `Discover` 方法检索 DISCOVER_PERFORMANCE_COUNTERS 架构行集的内容。|  
||会话|演示如何使用 XMLA `Discover` 方法检索 DISCOVER_SESSIONS 架构行集的内容。|  
||跟踪|演示如何使用 XMLA `Discover` 方法检索 DISCOVER_TRACES 架构行集的内容。|  
||事务|演示如何使用 XMLA `Discover` 方法检索 DISCOVER_TRANSACTIONS 架构行集的内容。|  
  
## <a name="see-also"></a>请参阅  
 [多维表达式 (MDX) 参考](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [数据挖掘扩展插件 (DMX) 参考](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Analysis Services 脚本语言&#40;ASSL&#41;引用](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [Analysis Services 脚本语言&#40;ASSL&#41;引用](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)  
  
  
