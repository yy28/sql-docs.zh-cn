---
title: "Excel 目标 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.exceldest.f1
- sql13.dts.designer.exceldestadapter.connection.f1
- sql13.dts.designer.exceldestadapter.mappings.f1
- sql13.dts.designer.exceldestadapter.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 69a0a8b907fcb45cf6ecd0576fb6fba04775d237
ms.contentlocale: zh-cn
ms.lasthandoff: 08/17/2017

---
# <a name="excel-destination"></a>Excel 目标
  Excel 目标将数据加载到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 工作簿中的工作表或范围中。  
  
## <a name="access-modes"></a>访问模式  
 Excel 目标为数据加载提供了三种数据访问模式：  
  
-   表或视图。  
  
-   变量中指定的表或视图。  
  
-   SQL 语句的运行结果。 查询可以是参数化查询。  
  
> [!IMPORTANT]  
>  在 Excel 中，工作表或范围等同于表或视图。 Excel 源和目标编辑器中可用表的列表仅显示现有的工作表（以追加到电子表格名称之后的 $ 符号为标识，如 Sheet1$）和指定范围（以 $ 符号的缺失为标识，如 MyRange）。  
  
## <a name="usage-considerations"></a>使用注意事项  
 Excel 连接管理器使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet 4.0 及其支持的 Excel ISAM（索引顺序存取方法）驱动程序来连接 Excel 数据源，并在 Excel 数据源中进行数据读写操作。  
  
 许多现有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知识库文章都记录了该访问接口和驱动程序的行为。虽然这些文章并非专门介绍 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或其前身 Data Transformation Services，但您仍可了解到一些可能导致意外结果的行为。 有关 Excel 驱动程序的使用及行为的一般信息，请参阅 [如何将 ADO 与来自 Visual Basic 或 VBA 的 Excel 数据一起使用](http://support.microsoft.com/kb/257819)。  
  
 在将数据保存到 Excel 目标时，Excel 驱动程序所附带的 Jet 访问接口的以下行为可以导致意外的结果。  
  
-   **保存文本数据**。 Excel 驱动程序将文本数据值保存到 Excel 目标时，驱动程序将在每个单元内的文本之前添加单引号字符 (') 以确保所保存的值将被解释为文本值。 如果拥有或要开发将读取或处理所保存的数据的其他应用程序，则可能需要包括特殊的措施，以处理位于每个文本值前面的单引号字符。  
  
     有关如何避免包括单引号的信息，请参阅 msdn.com 上的博客文章： [在 SSIS 包中使用 Excel 目标数据流组件时，单引号会在数据转换成 Excel 时追加到所有字符串](http://go.microsoft.com/fwlink/?LinkId=400876)。  
  
-   **保存 memo (ntext) 数据**。 若要将大于 255 个字符的字符串成功地保存到 Excel 列中，驱动程序必须将该目标列的数据类型识别为 **memo** ，而不是 **string**。 如果目标表中已存在数据行，则由驱动程序抽样的前几行的 memo 列中必须至少包含一个长度大于 255 个字符的值的实例。 如果目标表是在包设计或运行时创建的，则相应的 CREATE TABLE 语句必须使用 LONGTEXT（或其同义词之一）作为 memo 列的数据类型。  
  
-   **数据类型**。 Excel 驱动程序只识别有限的一组数据类型。 例如，所有数值列均解释为双精度 (DT_R8)，并且所有字符串列（除了 memo 列）均解释为 255 个字符的 Unicode 字符串 (DT_WSTR)。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 按如下所示方式映射 Excel 数据类型：  
  
    -   数值    双精度浮点 (DT_R8)  
  
    -   货币     货币 (DT_CY)  
  
    -   布尔     布尔 (DT_BOOL)  
  
    -   Date/time     **datetime** (DT_DATE)  
  
    -   字符串     Unicode 字符串，长度为 255 (DT_WSTR)  
  
    -   Memo     Unicode 文本流 (DT_NTEXT)  
  
-   **数据类型和长度转换**。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 不隐式转换数据类型。 因此，在将 Excel 数据加载到非 Excel 目标中之前，可能需要使用“派生列”或“数据转换”转换机制显式地转换它，或者在将其加载到 Excel 目标中之前将其转换为非 Excel 数据。 这种情况下，可能需要通过使用导入和导出向导（它将自动配置所需转换）来创建初始包。 下面是一些可能必需的转换的示例：  
  
    -   Unicode Excel 字符串列与具有特定代码页的非 Unicode 字符串列之间的转换。  
  
    -   在 255 个字符的 Excel 字符串列和不同长度的字符串列之间转换。  
  
    -   双精度 Excel 数值列与其他类型的数值列之间的转换。  
  
## <a name="configuration-of-the-excel-destination"></a>Excel 目标的配置  
 Excel 目标使用 Excel 连接管理器连接到数据源，而连接管理器指定要使用的工作簿文件。 有关详细信息，请参阅 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)。  
  
 Excel 目标具有一个常规输入和一个错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 **“高级编辑器”** 对话框反映了所有能以编程方式设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Excel 自定义属性](../../integration-services/data-flow/excel-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="related-tasks"></a>相关任务  
  
-   [连接到 Excel 工作簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
-   [使用 Foreach 循环容器循环遍历 Excel 文件和表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [设置数据流组件的属性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>相关内容  
  
-   dougbert.com 上的博客文章： [Integration Services 中的 Excel 第 1 部分（共 3 部分）：连接和组件](http://go.microsoft.com/fwlink/?LinkId=217674)。  
  
-   dougbert.com 上的博客文章： [Integration Services 中的 Excel 第 2 部分（共 3 部分）：表和数据类型](http://go.microsoft.com/fwlink/?LinkId=217675)。  
  
-   dougbert.com 上的博客文章： [Integration Services 中的 Excel 第 3 部分（共 3 部分）：问题和替代方案](http://go.microsoft.com/fwlink/?LinkId=217676)。  
  
## <a name="excel-destination-editor-connection-manager-page"></a>Excel 目标编辑器（“连接管理器”页）
  使用 **“Excel 目标编辑器”** 对话框的 **“连接管理器”** 页可以指定数据源信息和预览结果。 Excel 目标将数据加载到 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 工作簿中的工作表或指定范围。  
  
> [!NOTE]  
>  Excel 目标的 **CommandTimeout** 属性未在 **“Excel 目标编辑器”**中提供，但可以使用 **“高级编辑器”**进行设置。 另外，某些快速加载选项仅在 **“高级编辑器”**中提供。 有关这些属性的详细信息，请参阅 [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md)的“Excel 目标”部分。  
  
### <a name="static-options"></a>静态选项  
 **Excel 连接管理器**  
 从列表中选择现有的 Excel 连接管理器，或单击“新建”创建新连接。  
  
 **新建**  
 使用“Excel 连接管理器”对话框创建一个新连接管理器。  
  
 **数据访问模式**  
 指定从源选择数据的方法。  
  
|选项|Description|  
|------------|-----------------|  
|表或视图|将数据加载到 Excel 数据源中的工作表或指定范围。|  
|表名变量或视图名变量|在变量中指定工作表名称或范围名称。<br /><br /> **相关信息：** [在包中使用变量](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL 命令|使用 SQL 查询将数据加载到 Excel 目标中。|  
  
 **Excel 表的名称**  
 从下拉列表中选择 Excel 目标。 如果此列表为空，请单击 **“新建”**。  
  
 **新建**  
 单击“新建”将启动“创建表”对话框。 当您单击 **“确定”**时，此对话框将创建 **“Excel 连接管理器”** 指向的 Excel 文件。  
  
 **查看现有数据**  
 使用“预览查询结果”对话框预览结果。 预览最多可以显示 200 行。  
  
> [!WARNING]  
>  如果你选择的“Excel 连接管理器”指向的 Excel 文件不存在，则单击此按钮时你将看到一条错误消息。  
  
### <a name="data-access-mode-dynamic-options"></a>数据访问模式动态选项  
  
#### <a name="data-access-mode--table-or-view"></a>数据访问模式 = 表或视图  
 **Excel 表的名称**  
 从数据源中可用的工作表或指定范围列表中选择工作表或指定范围的名称。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>数据访问模式 = 表名变量或视图名变量  
 **变量名称**  
 选择包含工作表名称或指定范围名称的变量。  
  
#### <a name="data-access-mode--sql-command"></a>数据访问模式 = SQL 命令  
 **SQL 命令文本**  
 输入 SQL 查询的文本，通过单击“生成查询”来生成查询，或通过单击“浏览”定位到包含查询文本的文件。  
  
 **生成查询**  
 使用“查询生成器”对话框可直观地构造 SQL 查询。  
  
 **浏览**  
 使用“打开”对话框可定位到包含 SQL 查询文本的文件。  
  
 **分析查询**  
 验证查询文本的语法。  
  
## <a name="excel-destination-editor-mappings-page"></a>Excel 目标编辑器（“映射”页）
  可以使用 **“Excel 目标编辑器”** 对话框的 **“映射”** 页，将输入列映射到目标列。  
  
### <a name="options"></a>选项  
 **可用输入列**  
 查看可用输入列的列表。 使用拖放操作可以将表中的可用输入列映射到目标列。  
  
 **可用目标列**  
 查看可用目标列的列表。 使用拖放操作可以将表中的可用目标列映射到输入列。  
  
 **输入列**  
 查看从上表中选择的输入列。 可以通过使用 **“可用输入列”**列表来更改映射。  
  
 **目标列**  
 查看每个可用的目标列，包括已映射或未映射的目标列。  
  
## <a name="excel-destination-editor-error-output-page"></a>Excel 目标编辑器（“错误输出”页）
  可以使用 **“Excel 目标编辑器”** 对话框的 **“高级”** 页指定错误处理选项。  
  
### <a name="options"></a>选项  
 **输入或输出**  
 查看数据源的名称。  
  
 **列**  
 查看在“Excel 源编辑器”对话框中“连接管理器”节点上选择的外部（源）列。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [Excel 源](../../integration-services/data-flow/excel-source.md)   
 [Integration Services &#40;SSIS &#41;变量](../../integration-services/integration-services-ssis-variables.md)   
 [数据流](../../integration-services/data-flow/data-flow.md)   
 [Working with Excel Files with the Script Task](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  

