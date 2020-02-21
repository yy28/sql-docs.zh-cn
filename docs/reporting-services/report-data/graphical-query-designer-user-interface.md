---
title: 图形查询设计器用户界面 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
f1_keywords:
- "10012"
- sql13.rtp.rptdesigner.dataview.vdtquerydesigner.f1
helpviewer_keywords:
- graphical query designer [Reporting Services]
- data sources [Reporting Services], creating
- text-based query designer [Reporting Services]
- query designers [Reporting Services]
- Reporting Services, query designers
ms.assetid: 5022ae33-03a3-48de-8ac1-82742f48cebe
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ff907d83a4d793169872d5abaa059e8b6a1d91b3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "65572751"
---
# <a name="graphical-query-designer-user-interface"></a>图形查询设计器用户界面
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 同时提供了图形查询设计器和基于文本的查询设计器，用于创建在报表设计器中为报表数据集检索关系数据库中的数据的查询。 使用图形查询设计器能够以交互方式生成查询并查看数据源类型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle、OLE DB 和 ODBC 的结果。 使用基于文本的查询设计器可以指定多个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句、复杂的查询或命令语句以及基于表达式的查询。 有关详细信息，请参阅 [基于文本的查询设计器用户界面](https://msdn.microsoft.com/library/44b7c664-03aa-494e-a484-052b318e810c)。 有关使用特定数据源类型的详细信息，请参阅 [报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)。  
  
 。  
  
## <a name="graphical-query-designer"></a>图形查询设计器  
 此图形查询设计器支持三种类型的查询命令：Text、StoredProcedure 或 TableDirect。 为数据集创建查询之前，必须在 [“数据集属性”](https://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f) 对话框的“查询”页中选择一个命令类型选项。  
  
 以下是可用于查询类型的选项：  
  
-   **Text**：支持用于关系数据库数据源的标准 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询文本，其中包括 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Oracle 的数据处理扩展插件。  
  
-   **TableDirect** ：选择指定表中的所有列。 例如，对于名为 Customers 的表，这等同于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句 `SELECT * FROM Customers`。  
  
-   **StoredProcedure** ：支持对数据源中的存储过程的调用。 若要使用此选项，您必须已被数据库管理员授予对数据源中的存储过程的执行权限。  
  
 默认命令类型为 **“文本”**。  
  
> [!NOTE]  
>  不是所有的数据处理扩展插件都支持上述所有类型。 基础数据访问接口必须支持某个命令类型，该命令类型选项才可用。  
  
### <a name="command-type-text"></a>命令类型 Text  
 在 **“文本”** 类型中，图形查询设计器会显示四个区域，或四个窗格。 可以为 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询指定列、别名、排序值和筛选器值。 还可以查看根据您的选择生成的查询文本、运行查询并查看结果集。 下图显示了 4 个窗格。  
  
 ![用于 SQL 查询的图形查询设计器](../../reporting-services/report-data/media/rsqd-dsaw-sql.gif "用于 SQL 查询的图形查询设计器")  
  
 下表介绍了每个窗格的功能。  
  
|窗格|函数|  
|----------|--------------|  
|图表|显示查询中表的图形表示形式。 使用此窗格可以选择字段并定义表之间的关系。|  
|Grid|显示查询返回的字段列表。 使用此窗格可以定义别名、排序顺序、筛选器、组和参数。|  
|SQL|显示关系图窗格和网格窗格表示的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询。 使用此窗格可以用 [!INCLUDE[tsql](../../includes/tsql-md.md)]编写或更新查询。|  
|结果|显示查询的结果。 若要运行查询，请右键单击任意窗格，再单击“运行”，或者单击工具栏中的“运行”按钮。|  
  
 当您在前三个窗格的任意一个窗格中更改信息时，其他窗格中也会显示这些更改。 例如，如果在“关系图”窗格中添加了一个表，则将自动在 SQL 窗格的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询中添加该表。 如果在 SQL 窗格的查询中添加了一个字段，则将自动在“网格”窗格的列表中添加该字段并更新“关系图”窗格中的表。  
  
 有关详细信息，请参阅[查询和视图设计器工具（可视化数据库工具）](https://msdn.microsoft.com/library/12e4b5a5-b793-4b6c-a0e5-c450c49bf26f)。  
  
#### <a name="toolbar-for-the-graphical-query-designer"></a>图形查询设计器的工具栏  
 图形查询设计器工具栏提供了有助于您使用图形界面来设计 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询的按钮。  
  
|按钮|说明|  
|------------|-----------------|  
|**编辑为文本**|在基于文本的查询设计器和图形查询设计器之间切换。|  
|**导入**|从文件或报表中导入现有的查询。 仅支持 .sql 和 .rdl 文件类型。 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。|  
|![用于显示/隐藏“关系图”窗格的切换按钮](../../reporting-services/report-data/media/rsqdicon-showhidediagram.gif "用于显示/隐藏“关系图”窗格的切换按钮")|显示或隐藏“关系图”窗格。|  
|![用于显示或隐藏“网格”窗格的切换按钮](../../reporting-services/report-data/media/rsqdicon-showhidegrid.gif "用于显示或隐藏“网格”窗格的切换按钮")|显示或隐藏“网格”窗格。|  
|![用于显示或隐藏“SQL”窗格的切换按钮](../../reporting-services/report-data/media/rsqdicon-showhidesql.gif "用于显示或隐藏“SQL”窗格的切换按钮")|显示或隐藏 SQL 窗格。|  
|![用于显示或隐藏“结果”窗格的切换按钮](../../reporting-services/report-data/media/rsqdicon-showhideresult.gif "用于显示或隐藏“结果”窗格的切换按钮")|显示或隐藏“结果”窗格。|  
|![运行查询](../../reporting-services/report-data/media/rsqdicon-run.gif "运行查询")|运行查询。|  
|![用于在“SQL”窗格中验证 SQL 的按钮](../../reporting-services/report-data/media/rsqdicon-verifysql.gif "用于在“SQL”窗格中验证 SQL 的按钮")|检查查询文本的语法是否正确。|  
|![为选定字段设置按升序排序](../../reporting-services/report-data/media/rsqdicon-sortascending.gif "为选定字段设置按升序排序")|在“关系图”窗格中，将选定列的排序顺序设置为 **“升序排序”** 。|  
|![为选定字段设置按降序排序](../../reporting-services/report-data/media/rsqdicon-sortdescending.gif "为选定字段设置按降序排序")|在“关系图”窗格中，将选定列的排序顺序设置为 **“降序排序”** 。|  
|![删除选定字段的筛选器](../../reporting-services/report-data/media/rsqdicon-removefilter.gif "删除选定字段的筛选器")|在“关系图”窗格中，删除标记为有筛选器（![选定筛选器列旁边的筛选器图形](../../reporting-services/report-data/media/rsqdicon-filter.gif "选定筛选器列旁边的筛选器图形")）的选定列的筛选器。|  
|![对选定字段使用“分组依据”](../../reporting-services/report-data/media/rsqdicon-usegroupby.gif "对选定字段使用“分组依据”")|在“网格”窗格中显示或隐藏 **“分组依据”** 列。 当 **“分组依据”** 切换为开时，“网格”窗格中将出现以 **“分组依据”** 命名的额外列，并且查询中选定列的每个值都默认为 **“分组依据”**，这将导致选定列被包含在 SQL 文本的 Group By 子句中。 使用“分组依据”按钮自动添加 GROUP BY 子句，其中包括 SELECT 子句中的所有列。 当 SELECT 子句包含聚合函数调用（如 SUM(ColumnName)）时，如果想让它出现在结果集中，则需将每个非聚合列包含在 GROUP BY 子句中。<br /><br /> 若要出现在“结果”窗格中，查询中的每列都必须有一个定义用于计算要在“结果”窗格中显示的值的聚合函数，或者查询中的列都必须在 SQL 查询的 GROUP BY 子句中指定。|  
|![向“关系图”窗格中添加新表](../../reporting-services/report-data/media/rsqdicon-addtable.gif "向“关系图”窗格中添加新表")|从数据源向“关系图”窗格中添加新表。<br /><br /> **注意** ：添加新表时，查询设计器将尝试匹配来自数据源的外键关系。 添加表后，请确认表之间以链接形式表示的外键关系是正确的。|  
  
#### <a name="example"></a>示例  
 以下查询将从 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的 **Person** 表中返回姓氏列表：  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 可以通过 SQL 窗格运行存储过程。 以下查询将在 **数据库中运行存储过程** uspGetEmployeeManagers [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ：  
  
```  
EXEC uspGetEmployeeManagers '1';  
```  
  
### <a name="command-type-tabledirect"></a>命令类型 TableDirect  
 在 **TableDirect** 类型中，图形查询设计器将显示数据源中可用表的下拉列表和一个“结果”窗格。 如果选定一个表并单击 **“运行”** 按钮，将返回该表的所有列。  
  
> [!NOTE]  
>  只有 **OLE DB** 和 **ODBC** 数据源类型支持 TableDirect 功能。  
  
 下表介绍了每个窗格的功能。  
  
|窗格|函数|  
|----------|--------------|  
|表的下拉列表|列出来自数据源的所有可用表。 从列表中选择一项即可使其处于活动状态。|  
|结果|显示选定表的所有列。 若要运行表查询，请单击工具栏中的 **“运行”** 按钮。|  
  
#### <a name="toolbar-buttons-for-the-command-type-tabledirect"></a>命令类型 TableDirect 的工具栏按钮  
 图形查询设计器工具栏提供了数据源中的表的下拉列表。 下表列出了每个按钮及其功能。  
  
|按钮|说明|  
|------------|-----------------|  
|**编辑为文本**|在基于文本的查询设计器和图形查询设计器之间切换。|  
|**导入**|从文件或报表中导入现有的查询。 仅支持 .sql 和 .rdl 文件类型。 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。|  
|![“通用查询设计器”按钮图标](../../reporting-services/report-data/media/icongenericquerydesigner.gif "“通用查询设计器”按钮图标")|在通用查询设计器和图形查询设计器之间切换，同时保留查询文本或存储过程视图。|  
|![运行查询](../../reporting-services/report-data/media/rsqdicon-run.gif "运行查询")|选择选定表的所有列。|  
  
### <a name="command-type-storedprocedure"></a>命令类型 StoredProcedure  
 在 **StoredProcedure** 类型中，图形查询设计器将显示数据源中可用存储过程的下拉列表和一个“结果”窗格。 下表介绍了每个窗格的功能。  
  
|窗格|函数|  
|----------|--------------|  
|存储过程下拉列表|列出来自数据源的所有可用存储过程。 从列表中选择一项即可使其处于活动状态。|  
|结果|显示运行存储过程的结果。 若要运行选定的存储过程，请单击工具栏中的 **“运行”** 按钮。|  
  
#### <a name="toolbar-buttons-for-command-type-storedprocedure"></a>命令类型 StoredProcedure 的工具栏按钮  
 图形查询设计器工具栏提供了数据源中的存储过程的下拉列表。 下表列出了每个按钮及其功能。  
  
|按钮|说明|  
|------------|-----------------|  
|**编辑为文本**|在基于文本的查询设计器和图形查询设计器之间切换。|  
|**导入**|从文件或报表中导入现有的查询。 仅支持 .sql 和 .rdl 文件类型。 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。|  
|![运行查询](../../reporting-services/report-data/media/rsqdicon-run.gif "运行查询")|运行选定的存储过程。|  
|存储过程下拉列表|单击向下键，以显示来自数据源的可用存储过程的列表。 在列表中单击任一存储过程以将其选中。|  
  
#### <a name="example"></a>示例  
 以下存储过程将从 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中调用管理器的命令链列表。 该存储过程接受 *BusinessEntityID* 作为参数。 可输入任一小的整数。  
  
 `uspGetEmployeeManagers '1';`  
  
## <a name="see-also"></a>另请参阅  
 [查询设计工具 (SSRS)](../../reporting-services/report-data/query-design-tools-ssrs.md)   
 [报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [SQL Server 连接类型 (SSRS)](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)   
 [OLE DB 连接类型 (SSRS)](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)   
 [报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Oracle 连接类型 (SSRS)](../../reporting-services/report-data/oracle-connection-type-ssrs.md)   
 [RSReportDesigner 配置文件](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [设计查询和视图操作指南主题 (Visual Database Tools)](https://msdn.microsoft.com/library/200903f4-1208-4563-9dca-26aabaacfa20)  
  
  
