---
title: Excel 源 | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelsource.f1
- sql13.dts.designer.excelsourceadapter.connection.f1
- sql13.dts.designer.excelsourceadapter.columns.f1
- sql13.dts.designer.excelsourceadapter.erroroutput.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
caps.latest.revision: 60
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d275a24264a3ac174908f364c99975d4a0ec0014
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="excel-source"></a>Excel 源
  Excel 源从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 工作簿的工作表或范围中提取数据。  

> [!IMPORTANT]
> 有关连接到 Excel 文件的详细信息，以及从 Excel 文件加载数据或将数据加载到 Excel 文件的限制和已知问题，请参阅[使用 SQL Server Integration Services (SSIS) 从 Excel 加载数据或将数据加载到 Excel 中](../load-data-to-from-excel-with-ssis.md)。

## <a name="access-mode"></a>访问模式
 Excel 源提供了四种提取数据的数据访问方式：  
  
-   表或视图。  
  
-   变量中指定的表或视图。  
  
-   SQL 语句的运行结果。 查询可以是参数化查询。  
  
-   存储在变量中的 SQL 语句的运行结果。  
  
 Excel 源使用 Excel 连接管理器与数据源建立连接，连接管理器可指定要使用的工作簿文件。 有关详细信息，请参阅 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)。  
  
 Excel 源有一个常规输出和一个错误输出。  
  
## <a name="usage-considerations"></a>使用注意事项  
 Excel 连接管理器使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet 4.0 及其支持的 Excel ISAM（索引顺序存取方法）驱动程序来连接 Excel 数据源，并在 Excel 数据源中进行数据读写操作。  
  
 许多现有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知识库文章都记录了该访问接口和驱动程序的行为。虽然这些文章并非专门介绍 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或其前身 Data Transformation Services，但您仍可了解到一些可能导致意外结果的行为。 有关 Excel 驱动程序的使用及行为的一般信息，请参阅 [如何将 ADO 与来自 Visual Basic 或 VBA 的 Excel 数据一起使用](http://support.microsoft.com/kb/257819)。  
  
 当从 Excel 数据源读取数据时，Jet 访问接口和 Excel 驱动程序的下列行为可能会导致意外结果。  
  
-   **数据源**。 Excel 工作簿中的数据源可以是工作表（必须追加 $ 符号，如 Sheet1$）或命名区域（如 MyRange）。 在 SQL 语句中，工作表的名称必须加以分隔（如 [Sheet1$]），以避免 $ 符号引起语法错误。 查询生成器可自动添加这些分隔符。 指定工作表或范围时，该驱动程序将读取从工作表或范围左上角第一个非空单元开始的连续单元块。 因此，源数据中不能有空行，在标题或页眉行与数据行之间也不能有空行。  
  
-   **缺少值**。 Excel 驱动程序读取指定源中一定数量的行（默认情况下为 8 行）以推测每列的数据类型。 如果推测出列可能包含混合数据类型（尤其是混合了文本数据的数值数据时），驱动程序将决定采用占多数的数据类型，并对包含其他类型数据的单元返回 Null 值。 （如果各种数据类型的数量相当，则采用数值类型。）Excel 工作表中大部分单元格格式设置选项不会影响此数据类型判断。 可以通过指定导入模式来修改 Excel 驱动程序的此行为。 若要指定导入模式，请在“属性”窗口中将 **IMEX=1** 添加到 Excel 连接管理器的连接字符串内的扩展属性值中。 有关详细信息，请参阅 [PRB: Excel Values Returned as NULL Using DAO OpenRecordset（PRB：使用 DAO OpenRecordset 返回的 Excel NULL 值）](http://support.microsoft.com/kb/194124)。  
  
-   **截断的文本**。 驱动程序在确定 Excel 列是否包含文本数据时，它将基于采样的最长值来选择数据类型（字符串或 memo）。 如果驱动程序没有在其采样的行中发现任何长于 255 个字符的值，那么它会将该列视为 255 个字符的字符串的列而不是 memo 列。 因此，长度超过 255 个字符的值可能会被截断。 若要从 memo 列导入数据而不发生截断，必须确保至少一个采样行中的 memo 列包含的值的长度超过 255 个字符，否则必须增加驱动程序采样的行数，使其包括这样的行。 你可以通过增加 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Jet\4.0\Engines\Excel** 注册表项下的 **TypeGuessRows** 的值来增加用作示例的行数。 有关详细信息，请参阅 [PRB：从 Jet 4.0 OLEDB 源传输数据失败并出现错误](http://support.microsoft.com/kb/281517)。  
  
-   **数据类型**。 Excel 驱动程序只识别有限的一组数据类型。 例如，所有数值列均解释为双精度 (DT_R8)，并且所有字符串列（除了 memo 列）均解释为 255 个字符的 Unicode 字符串 (DT_WSTR)。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 按如下所示方式映射 Excel 数据类型：  
  
    -   数值 – 双精度浮点 (DT_R8)  
  
    -   货币 – 货币 (DT_CY)  
  
    -   布尔 – 布尔 (DT_BOOL)  
  
    -   日期/时间 – **日期** (DT_DATE)  
  
    -   字符串 – Unicode 字符串，长度为 255 (DT_WSTR)  
  
    -   Memo – Unicode 文本流 (DT_NTEXT)  
  
-   **数据类型和长度转换**。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 不隐式转换数据类型。 因此，在将其加载到非 Excel 目标之前，可能需要使用“派生列”或“数据转换”转换来显式转换 Excel 数据，或在将它加载到 Excel 目标之前，对非 Excel 数据进行转换。 这种情况下，可能需要通过使用导入和导出向导（它将自动配置所需转换）来创建初始包。 下面是一些可能必需的转换的示例：  
  
    -   Unicode Excel 字符串列与具有特定代码页的非 Unicode 字符串列之间的转换  
  
    -   在 255 个字符的 Excel 字符串列和不同长度的字符串列之间转换  
  
    -   双精度 Excel 数值列与其他类型的数值列之间的转换  
  
## <a name="excel-source-configuration"></a>Excel 源配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 **“高级编辑器”** 对话框反映了所有能以编程方式设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Excel 自定义属性](../../integration-services/data-flow/excel-custom-properties.md)  
  
 有关循环遍历 Excel 文件中的某个组的信息，请参阅 [使用 Foreach 循环容器，循环遍历 Excel 文件和表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [将查询参数映射到数据流组件中的变量](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [设置数据流组件的属性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [为合并转换和合并联接转换排序数据](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
-   [使用 Foreach 循环容器循环遍历 Excel 文件和表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
## <a name="excel-source-editor-connection-manager-page"></a>Excel 源编辑器（“连接管理器”页）
  使用 **“Excel 源编辑器”** 对话框的 **“连接管理器”** 节点可以为源选择要使用的 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 工作簿。 Excel 源从现有工作簿中的工作表或指定范围中读取数据。  
  
> [!NOTE]  
>  Excel 源的 **CommandTimeout** 属性未在 **“Excel 源编辑器”**中提供，但可以使用 **“高级编辑器”**进行设置。 有关此属性的详细信息，请参阅 [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md)的“Excel 源”部分。  
  
### <a name="static-options"></a>静态选项  
 **“无缓存”**  
 从列表中选择现有的 Excel 连接管理器，或单击“新建”创建新连接。  
  
 **新建**  
 使用“Excel 连接管理器”对话框创建一个新连接管理器。  
  
 **数据访问模式**  
 指定从源选择数据的方法。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|表或视图|从 Excel 文件的工作表或指定范围中检索数据。|  
|表名变量或视图名变量|在变量中指定工作表名称或范围名称。<br /><br /> **相关信息：** [在包中使用变量](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL 命令|使用 SQL 查询从 Excel 文件中检索数据。 |  
|变量中的 SQL 命令|在变量中指定 SQL 查询文本。|  
  
 **预览**  
 通过使用“数据视图”对话框预览结果。 预览最多可以显示 200 行。  
  
### <a name="data-access-mode-dynamic-options"></a>数据访问模式动态选项  
  
#### <a name="data-access-mode--table-or-view"></a>数据访问模式 = 表或视图  
 **Excel 表的名称**  
 从 Excel 工作簿可用的工作表或指定范围中选择工作表或指定范围的名称。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>数据访问模式 = 表名变量或视图名变量  
 **变量名称**  
 选择包含工作表名称或指定范围名称的变量。  
  
#### <a name="data-access-mode--sql-command"></a>数据访问模式 = SQL 命令  
 **SQL 命令文本**  
 输入 SQL 查询的文本，通过单击“生成查询”来生成查询，或通过单击“浏览”浏览至包含查询文本的文件。  
  
 **Parameters**  
 如果已经在参数化查询文本中使用 ? 作为参数占位符输入了参数化查询，请使用 **“设置查询参数”** 对话框将查询输入参数映射到包变量。  
  
 **生成查询**  
 使用“查询生成器”对话框可直观地构造 SQL 查询。  
  
 **“浏览”**  
 使用“打开”对话框可定位到包含 SQL 查询文本的文件。  
  
 **分析查询**  
 验证查询文本的语法。  
  
#### <a name="data-access-mode--sql-command-from-variable"></a>数据访问模式 = 变量中的 SQL 命令  
 **变量名称**  
 选择包含 SQL 查询文本的变量。  
  
## <a name="excel-source-editor-columns-page"></a>Excel 源编辑器（“列”页）
  可以使用“Excel 源编辑器”对话框的“列”页，将输出列映射到每个外部（源）列。  
  
### <a name="options"></a>“常规”  
 **可用外部列**  
 查看数据源中可用外部列的列表。 无法使用此表添加或删除列。  
  
 **“外部列”**  
 按任务读取外部（源）列的顺序查看这些列。 首先在上面讨论的表中清除所选择的列，然后以不同的顺序从列表中选择外部列，即可更改顺序。  
  
 **输出列**  
 为每个输出列提供唯一的名称。 默认值为所选外部（源）列的名称；不过，您也可以任选一个唯一的描述性名称。 所提供的名称将在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中显示。  
  
## <a name="excel-source-editor-error-output-page"></a>Excel 源编辑器（“错误输出”页）
  可以使用 **“Excel 源编辑器”** 对话框的 **“错误输出”** 页选择错误处理选项以及设置错误输出列的属性。  
  
### <a name="options"></a>“常规”  
 **输入或输出**  
 查看数据源的名称。  
  
 **列**  
 查看在“Excel 源编辑器”对话框中“连接管理器”页上选择的外部（源）列。  
  
 **错误**  
 指定发生错误时应执行的操作：忽略失败、重定向行或使组件失败。  
  
 **相关主题：**[数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **截断**  
 指定发生截断时应执行的操作：忽略失败、重定向行或使组件失败。  
  
 **Description**  
 查看对错误的说明。  
  
 **将此值设置到选定的单元格**  
 指定发生错误或截断时应对所有选定单元格执行的操作：忽略失败、重定向行或使组件失败。  
  
 **应用**  
 将错误处理选项应用到选定的单元格。  
  
## <a name="related-content"></a>相关内容  
[使用 SQL Server Integration Services (SSIS) 从 Excel 加载数据或将数据加载到 Excel 中](../load-data-to-from-excel-with-ssis.md)
[Excel 目标提供程序](excel-destination.md)  
[Excel 连接管理器](../connection-manager/excel-connection-manager.md)
