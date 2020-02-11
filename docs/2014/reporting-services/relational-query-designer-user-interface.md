---
title: 关系查询设计器用户界面 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4f8aa192-e6fc-4b4e-b107-5a5372ac31d9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 45f4b0b09c5f99a1dc561fdba40a659b7f0012d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68891139"
---
# <a name="relational-query-designer-user-interface"></a>关系查询设计器用户界面
  中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]报表设计器同时提供了图形查询设计器和基于文本的查询设计器，可帮助您创建一个查询，该查询指定要[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]从[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)]报表数据集和为报表数据集检索的数据。 使用图形查询设计器可以浏览元数据、以交互方式生成查询，还可以查看查询结果。 使用基于文本的查询设计器可以查看图形查询设计器生成的查询，也可以修改查询。 您还可以从文件或报表中导入现有的查询。  
  
> [!NOTE]  
>  用来编写查询以从 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 和 [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)] 检索数据的图形查询设计器与用于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的查询设计器不同。 若要编写查询以从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 检索数据，您要使用 Visual Studio 提供的 [!INCLUDE[vspnvdt](../includes/vspnvdt-md.md)]。 有关详细信息，请参阅 [Graphical Query Designer User Interface](report-data/graphical-query-designer-user-interface.md)。  
  
> [!IMPORTANT]  
>  用户创建和运行查询时访问数据源。 您应授予对数据源的最小权限（如只读权限）。  
  
## <a name="graphical-query-designer"></a>图形查询设计器  
 在图形查询设计器中，您可以浏览数据库表和视图，还可以交互式生成 SQL SELECT 语句，以便指定要从中检索数据集数据的数据库表和列。 您可以选择要包括在数据集中的字段，或者指定限制数据集中数据的筛选器。 可以指定将筛选器作为参数并在运行时提供筛选器的值。 如果选择多个相关表，则查询设计器将描述由两个表构成的集合之间的关系。  
  
 图形查询设计器分为三个区域。 根据查询是使用表/视图还是存储过程/表值函数，查询设计器的布局有所不同。  
  
> [!NOTE]  
>  
  [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)] 不支持存储过程或表值函数。  
  
 下图显示了用于表或视图的图形查询设计器。  
  
 ![用于查询的图形设计器](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqd-relational-graphical.gif "用于查询的图形设计器")  
  
 下图显示了用于存储过程或表值函数的图形查询设计器。  
  
 ![图形查询设计器中的存储过程](https://docs.microsoft.com/analysis-services/analysis-services/media/rs-relational-graphical-sp.gif "图形查询设计器中的存储过程")  
  
 下表介绍了每个窗格的功能。  
  
 [数据库视图](#DatabaseView)  
 显示按数据库架构组织的表、视图、存储过程和表值函数的层次结构视图。  
  
 [所选字段](#SelectedFields)  
 在“数据库视图”窗格中显示选定项中的数据库字段名称列表。 这些字段将成为报表数据集的字段集合。  
  
 [函数参数](#FunctionParameters)  
 在“数据库视图”窗格中显示存储过程或表值函数的输入参数列表。  
  
 [关系](#Relationships)  
 在“数据库视图”窗格中显示通过表或视图中的选定字段推断出的关系或您手动创建的关系的列表。  
  
 [应用的筛选器](#AppliedFilters)  
 在“数据库视图”中显示表或视图的字段列表和筛选条件。  
  
 [查询结果](#QueryResults)  
 显示自动生成的查询的结果集示例数据。  
  
###  <a name="DatabaseView"></a>"数据库视图" 窗格  
 “数据库视图”窗格显示您有权查看的数据库对象的元数据，该元数据取决于数据源连接和凭据。 层次结构视图显示按数据库架构组织的数据库对象。 展开每个架构的节点可查看表、视图、存储过程及表值函数。 展开表或视图可显示列。  
  
###  <a name="SelectedFields"></a>"所选字段" 窗格  
 “所选字段”窗格显示报表数据集中的字段以及要包括在查询中的分组和聚合。  
  
 显示下列选项：  
  
-   **所选字段**显示您为表或视图选择的数据库字段，或者为存储过程或表值函数选择的输入参数。 此窗格中显示的字段将成为报表数据集的字段集合。  
  
     使用“报表数据”窗格可查看报表数据集的字段集合。 这些字段表示当您查看报表时可在表、图表及其他报表项中显示的数据。  
  
-   **分组和聚合**在查询中切换分组和聚合的使用。 如果您在添加分组和聚合后禁用分组和聚合功能，则将删除所添加的分组和聚合。 文本“(无)”表示没有使用任何分组和聚合****。 如果您再次启用分组和聚合功能，则将还原之前的分组和聚合。  
  
-   **删除字段**删除所选字段。  
  
#### <a name="group-and-aggregate"></a>分组和聚合  
 查询包含大表的数据库时可能会返回很多数据行，这些数据行由于数量过多以至于在报表中没有什么用处，此外，这种查询对于传输大量数据的网络和处理报表的报表服务器的性能会造成负面影响。 为了限制数据行的数量，查询可以包含对数据库服务器中的数据进行汇总的 SQL 聚合。 SQL 聚合不同于客户端聚合，它在呈现报表时应用。  
  
 聚合功能可对数据进行汇总，并且数据也会进行分组，以支持传递汇总数据的聚合。 在查询中使用聚合时，查询返回的其他字段将自动进行分组，并且查询包括 SQL GROUP BY 子句。 可以通过仅在 **“分组和聚合”** 列表中使用 **“分组依据”** 选项来汇总数据，而不必添加聚合。 许多聚合都包括使用 DISTINCT 关键字的版本。 包括 DISTINCT 可消除重复的值。  
  
 [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)]使用[!INCLUDE[tsql](../includes/tsql-md.md)]和[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)]使用[!INCLUDE[DWsql](../includes/dwsql-md.md)]。 SQL 语言的这两种分支都支持查询设计器提供的子句、关键字和聚合。  
  
 有关 [!INCLUDE[tsql](../includes/tsql-md.md)] 的详细信息，请参阅 msdn.microsoft.com 上 [](/sql/t-sql/language-reference)联机丛书中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [Transact-SQL 引用（数据库引擎）](https://go.microsoft.com/fwlink/?LinkId=141687)。  
  
 下表列出各种聚合并提供其简要说明。  
  
|Aggregate|说明|  
|---------------|-----------------|  
|Avg|返回组中各值的平均值。 实现 SQL AVG 聚合。|  
|Count|返回组中项数。 实现 SQL COUNT 聚合。|  
|Count Big|返回组中的项数。 这是 SQL COUNT_BIG 聚合。 COUNT 和 COUNT_BIG 之间的区别是 COUNT_BIG 始终返回一个 `bigint` 数据类型的值。|  
|Min|返回组中的最小值。 实现 SQL MIN 聚合。|  
|Max|返回组中的最大值。 实现 SQL MAX 聚合。|  
|StDev|返回组中所有值的统计标准偏差。 实现 SQL STDEV 聚合。|  
|StDevP|返回指定组中所有值的总体标准偏差。 实现 SQL STDEVP 聚合。|  
|SUM|返回组中所有值的总和。 实现 SQL SUM 聚合。|  
|Var|返回组中所有值的方差。 实现 SQL VAR 聚合。|  
|VarP|返回组中所有值的总体方差。 实现 SQL VARP 聚合。|  
|Avg Distinct|返回唯一项的均值。 实现 AVG 聚合和 DISTINCT 关键字的组合。|  
|Count Distinct|返回唯一项的计数。 实现 COUNT 聚合和 DISTINCT 关键字的组合。|  
|Count Big Distinct|返回组中唯一项的计数。 实现 COUNT_BIG 聚合和 DISTINCT 关键字的组合。|  
|StDev Distinct|返回唯一项的标准偏差。 实现 STDEV 聚合和 DISTINCT 关键字的组合。|  
|StDevP Distinct|返回唯一项的标准偏差。 实现 STDEVP 聚合和 DISTINCT 关键字的组合。|  
|Sum Distinct|返回唯一项的总和。 实现 SUM 聚合和 DISTINCT 关键字的组合。|  
|Var Distinct|返回唯一项的方差。 实现 VAR 聚合和 DISTINCT 关键字的组合。|  
|VarP Distinct|返回唯一项的方差。 实现 VARP 聚合和 DISTINCT 关键字的组合。|  
  
###  <a name="FunctionParameters"></a>函数参数窗格  
 “函数参数”窗格显示存储过程或表值函数的参数。 显示以下列：  
  
-   **参数名称**显示由存储过程或表值函数定义的参数的名称。  
  
-   **值**在运行查询时用于检索要在设计时在 "查询结果" 窗格中显示的数据的参数值。 当报表在运行时运行时不使用此值。  
  
###  <a name="Relationships"></a>关系窗格  
 “关系”窗格显示联接关系。 可以根据从数据库元数据检索的外键关系自动检测到关系，也可以手动创建关系。  
  
 显示下列选项：  
  
-   **自动检测**切换自动检测功能，该功能会自动创建表之间的关系。 如果启用自动检测，则查询设计器将根据表中的外键创建关系；否则，您必须手动创建关系。 当您在 **“数据库视图”** 窗格中选择表时，自动检测将尝试自动创建关系。 如果您在手动创建联接后启用自动检测，则这些联接将被丢弃。  
  
    > [!IMPORTANT]  
    >  与 [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)] 一起使用时，由于不会提供创建联接所需的元数据，因此无法自动检测到关系。 如果您的查询从 [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)]中检索数据，则必须手动创建所有表联接。  
  
-   **添加关系**向**关系**列表中添加关系。  
  
     如果启用自动检测，则查询中使用的列所在的表将会自动添加到 **“关系”** 列表。 当自动检测确定两个表相关时，会将其中一个表添加到 **“左表”** 列，并将另一个表添加到 **“右表”** 列，并在这两个表之间创建内部联接。 每个关系都会在查询中生成一个 JOIN 子句。 如果各表不相关，则所有表都将列在 **“左表”** 列，并且 **“联接类型”** 列指示对应表与其他表无关。 如果启用自动检测，则无法在自动检测已确定无关的表之间手动添加关系。  
  
     如果禁用自动检测，则可以添加和更改表之间的关系。 单击 **“编辑字段”** 可指定要用于联接两个表的字段。  
  
     关系在 **“关系”** 列表中显示的顺序即是将在查询中执行联接的顺序。 您可以通过在列表中上下移动关系来更改关系的顺序。  
  
     当在查询中使用多个关系时，除第一个关系以外的所有关系中都必须有一个表被前一个关系引用。  
  
     如果某个关系中的两个表都被前一个关系引用，则该关系将不生成单独的联接子句，而是将联接条件添加到为上一个关系生成的联接子句中。 联接类型可从引用相同表的上一个关系中推断出来。  
  
-   **编辑字段**打开 "**编辑相关字段**" 对话框，您可以在其中添加和修改表之间的关系。 在左表和右表中选择要联接的字段。 可以将左表和右表中的多个字段联接起来，以便在一个关系中指定多个联接条件。 联接左表和右表的两个字段的名称不必相同。 联接字段的数据类型必须兼容。  
  
-   **删除关系** 删除所选的关系 **。**  
  
-   "**上移** **" 和 "下移"** 可在**关系**列表中向上或向下移动关系。 关系在查询中的放置顺序会影响到查询结果。 关系将按其在 **“关系”** 列表中的显示顺序添加到查询中。  
  
 显示以下列：  
  
-   **左表**显示作为联接关系一部分的第一个表的名称。  
  
-   **联接类型**显示自动生成的查询中使用的 SQL JOIN 语句的类型。 默认情况下，如果检测到外键约束，将会使用 INNER JOIN。 其他联接类型可以为 LEFT JOIN 或 RIGHT JOIN。 如果不应用所有这些联接类型，则 **“联接类型”** 列将显示 **“无关”**。 不会为无关表创建 CROSS JOIN 联接；相反，您必须通过联接左表和右表中的列来手动创建关系。 有关 JOIN 的类型的详细信息，请参阅 msdn.microsoft.com 上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [联机丛书](https://go.microsoft.com/fwlink/?LinkId=141687) 中的“JOIN Fundamentals”（JOIN 基础知识）。  
  
-   **右表**显示联接关系中第二个表的名称。  
  
-   **联接字段**列出联接字段对，如果某个关系具有多个联接条件，则联接字段对用逗号（，）分隔。  
  
###  <a name="AppliedFilters"></a>应用的筛选器窗格  
 “应用的筛选器”窗格显示用于限定在运行时检索的数据行数的条件。 此窗格中指定的条件用于生成 SQL WHERE 子句。 如果选择了参数选项，则会自动创建报表参数。 通过基于查询参数的报表参数，用户可为查询指定值，以便控制报表中的数据。  
  
 显示以下列：  
  
-   **字段名称**显示要将条件应用于的字段的名称。  
  
-   **运算符**显示要在筛选器表达式中使用的操作。  
  
-   **值**显示要在筛选表达式中使用的值。  
  
-   **参数**显示用于向查询添加查询参数的选项。 使用“数据集属性”可查看查询参数与报表参数之间的关系。  
  
###  <a name="QueryResults"></a>查询结果窗格  
 “查询结果”窗格显示由其他窗格中的选项指定并且自动生成的查询的结果。 结果集中的列是您在“所选字段”窗格中指定的字段，行数据受限于您在“应用的筛选器”窗格中指定的筛选器。 如果查询包括聚合，则结果集将包括新的聚合列。 例如，如果使用 Count 聚合对列 **Color** 进行聚合，则查询结果将包括新列。 默认情况下，此列名为 **Count_Color**。  
  
 此数据表示在运行查询时数据源中的值。 此数据未保存在报表定义中。报表中的实际数据是在处理报表时进行检索的。  
  
 结果集中的排序顺序取决于从数据源检索数据的顺序。 可以通过修改查询来更改排序顺序，也可以在为报表检索数据后更改。  
  
### <a name="graphical-query-designer-toolbar"></a>图形查询设计器工具栏  
 关系查询设计器工作栏提供了以下按钮，帮助您指定或查看查询结果。  
  
|按钮|说明|  
|------------|-----------------|  
|**编辑为文本**|切换到基于文本的查询设计器，可查看自动生成的查询，也可以修改查询。|  
|**Import**|从文件或报表中导入现有的查询。 支持 .sql 和 .rdl 文件类型。|  
|**运行查询**|运行查询。 “查询结果”窗格显示结果集。|  
  
## <a name="understanding-automatically-generated-queries"></a>了解自动生成的查询  
 当您在“数据库视图”窗格中选择表和列或存储过程及视图时，查询设计器将从数据库架构中检索主键与外键的基本关系。 通过分析这些关系，查询设计器会检测到两个表之间的关系并将联接添加到查询中。 然后，您即可通过添加分组和聚合、添加或更改关系并添加筛选器来修改查询。 若要查看显示要从中检索数据的列、表之间的联接以及任何分组或聚合的查询文本，请单击 **“编辑为文本”**。  
  
## <a name="text-based-query-designer"></a>基于文本的查询设计器  
 若要最大限度地控制查询，请使用基于文本的查询设计器。 若要切换到基于文本的查询设计器，请在工具栏中单击“编辑为文本”****。 在基于文本的查询设计器中编辑查询之后，就不能再使用关系查询设计器了。 随后，查询将始终在基于文本的查询设计器中打开。 有关详细信息，请参阅 [基于文本的查询设计器用户界面](../../2014/reporting-services/text-based-query-designer-user-interface.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 查询设计器](../../2014/reporting-services/reporting-services-query-designers.md)  
  
  
