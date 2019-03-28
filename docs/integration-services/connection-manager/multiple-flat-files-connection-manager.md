---
title: 多平面文件连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.multifile.advanced.f1
- sql13.dts.designer.multifile.columns.f1
- sql13.dts.designer.multifile.general.f1
- sql13.dts.designer.multifile.preview.f1
helpviewer_keywords:
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0e81e43aa0eafb76b107c30b2bdd07a0a70b60fd
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58275741"
---
# <a name="multiple-flat-files-connection-manager"></a>多平面文件连接管理器
  多平面文件连接管理器使包可以访问多个平面文件中的数据。 例如，数据流任务在循环容器（例如 For 循环容器）内时，平面文件源可以使用多平面文件连接管理器。 在容器的每个循环中，平面文件源从多平面文件连接管理器提供的下一个文件名加载数据。  
  
 将多平面文件连接管理器添加到包时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时解析多平面文件连接的连接管理器，同时还会设置该多平面文件连接管理器的属性，并将该多平面文件连接管理器添加到包的 **Connections** 集合。  
  
 该连接管理器的 **ConnectionManagerType** 属性设置为 **MULTIFLATFILE**。  
  
 可以按下列方式配置多平面文件连接管理器：  
  
-   指定要使用的文件、区域设置和代码页。 区域设置用于解释受区域设置影响的数据（如日期），代码页用于将字符串数据转换为 Unicode。  
  
-   指定文件格式。 可以使用带分隔符、具有固定宽度或右边未对齐的文件格式。  
  
-   指定标题行、数据流和列分隔符。 列分隔符可以在文件级别设置，而在列级别被覆盖。  
  
-   指示文件中的第一行是否包含列名称。  
  
-   指定文本限定符。 可以将每一列配置为识别文本限定符。  
  
-   对各列设置诸如名称、数据类型和最大宽度等属性。  
  
 当多平面文件连接管理器引用多个文件时，文件的路径由竖线 (|) 分隔。 连接管理器的 **ConnectionString** 属性的格式如下：  
  
 \<路径>|\<路径>  
  
 也可以使用通配符来指定多个文件。 例如，若要引用 C 驱动器上的所有文本文件，可以将 **ConnectionString** 属性的值设置为 C:\\*.txt。  
  
 如果多平面文件连接管理器引用多个文件，则所有文件必须具有相同格式。  
  
 默认情况下，多平面文件连接管理器将字符串列的长度设置为 50 个字符。 在 **“多个平面文件连接管理器编辑器”** 对话框中，可以计算示例数据，并自动调整这些列的长度大小，以防止发生数据截断或超过列宽的情况。 除非在平面文件源或转换过程中调整列长度的大小，否则列长度将在整个数据流中保持不变。 如果这些列映射到更窄的目标列，则用户界面将显示警告，在运行时，则可能由于数据截断而发生错误。 可以在平面文件连接管理器、平面文件源或转换过程中调整列的大小，以便与目标列兼容。 若要修改输出列的长度，请在 **“高级编辑器”** 对话框中的 **“输入属性和输出属性”** 选项卡上设置输出列的 **Length** 属性。  
  
 在已添加并配置了使用连接管理器的平面文件源之后，如果在多平面文件连接管理器中更新了列长度，则不必在平面文件源中手动调整输出列的大小。 打开 **“平面文件源”** 对话框时，平面文件源将提供同步列元数据的选项。  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>多平面文件连接管理器的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
## <a name="multiple-flat-files-connection-manager-editor-general-page"></a>多平面文件连接管理器编辑器（“常规”页）
  可以使用 **“多平面文件连接管理器编辑器”** 对话框的 **“常规”** 页，选择一组具有相同数据格式的文件并指定其数据格式。 多平面文件连接使得数据包可以连接到具有相同格式的一组文本文件。  
  
 若要了解有关多平面文件连接管理器的详细信息，请参阅 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)。  
  
### <a name="options"></a>选项  
 **连接管理器名称**  
 为工作流中的“多平面文件连接”提供一个唯一名称。 所提供的名称将在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中显示。  
  
 **Description**  
 描述此连接。 最好按照连接的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
 **文件名**  
 键入要在“多平面文件连接”中使用的路径和文件名。 可以通过使用通配符指定多个文件，如示例“C:\\*.txt”中一样，也可以通过使用竖线 (|) 来分隔多个文件名。 所有文件的数据格式必须相同。  
  
 **“浏览”**  
 通过定位文件来指定要在“多平面文件连接”中使用的文件名。 您可以选择多个文件。 所有文件的数据格式必须相同。  
  
 **区域设置**  
 指定与排序以及日期和时间转换设置相关的区域设置。  
  
 **Unicode**  
 指示是否使用 Unicode。 如果使用 Unicode，将不能指定代码页。  
  
 **代码页**  
 指定非 Unicode 文本的代码页。  
  
 **格式**  
 指示是否使用带分隔符、固定宽度或右边未对齐的格式。 所有文件的数据格式必须相同。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|带分隔符|各列之间由在 **“列”** 页上指定的分隔符隔开。|  
|固定宽度|列的宽度固定，通过在 **“列”** 页上拖动标记线即可指定列的宽度。|  
|右边未对齐|在右边未对齐的文件中，除最后一列之外的每一列的宽度都固定，而最后一列由 **“列”** 页上指定的行分隔符进行分隔。|  
  
 **文本限定符**  
 指定要使用的文本限定符。 例如，您可以指定将文本包含在引号中。  
  
 **标题行分隔符**  
 从标题行的分隔符列表中选择，或输入分隔符文本。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**{CR}{LF}**|标题行由回车符和换行符的组合分隔。|  
|**{CR}**|标题行由回车符分隔。|  
|**{LF}**|标题行由换行符分隔。|  
|**分号 {;}**|标题行由分号分隔。|  
|**冒号 {:}**|标题行由冒号分隔。|  
|**逗号 {,}**|标题行由逗号分隔。|  
|**制表符 {t}**|标题行由制表符分隔。|  
|**竖线 {|}**。|标题行由竖线分隔。|  
  
 **要跳过的标题行数**  
 指定要跳过的标题行数（如果有的话）。  
  
 **第一个数据行中的列名称**  
 指示在第一个数据行中是否要求列名或提供列名。  
  
## <a name="multiple-flat-files-connection-manager-editor-columns-page"></a>多平面文件连接管理器编辑器（“列”页）
  可以使用 **“多平面文件连接管理器编辑器”** 对话框的 **“列”** 节点指定行和列的信息，以及预览选定的第一个文件。  
  
 若要了解有关多平面文件连接管理器的详细信息，请参阅 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)。  
  
### <a name="static-options"></a>静态选项  
 **连接管理器名称**  
 为工作流中的“多平面文件连接”提供一个唯一名称。 所提供的名称将在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中显示。  
  
 **Description**  
 描述此连接。 最好按照连接的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
### <a name="flat-file-format-dynamic-options"></a>平面文件格式动态选项  
  
#### <a name="format--delimited"></a>格式 = 带分隔符  
 **行分隔符**  
 从可用行分隔符的列表中选择，或输入分隔符文本。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**{CR}{LF}**|行由回车符和换行符的组合分隔。|  
|**{CR}**|行由回车符分隔。|  
|**{LF}**|行由换行符分隔。|  
|**分号 {;}**|行由分号分隔。|  
|**冒号 {:}**|行由冒号分隔。|  
|**逗号 {,}**|行由逗号分隔。|  
|**制表符 {t}**|行由制表符分隔。|  
|**竖线 {|}**。|行由竖线分隔。|  
  
 **列分隔符**  
 从可用列分隔符的列表中选择，或输入分隔符文本。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**{CR}{LF}**|列由回车符和换行符的组合分隔。|  
|**{CR}**|列由回车符分隔。|  
|**{LF}**|列由换行符分隔。|  
|**分号 {;}**|列由分号分隔。|  
|**冒号 {:}**|列由冒号分隔。|  
|**逗号 {,}**|列由逗号分隔。|  
|**制表符 {t}**|列由制表符分隔。|  
|**竖线 {|}**。|列由竖线分隔。|  
  
 **重置列**  
 通过单击“重置列”可以删除除原始列之外的所有列。  
  
#### <a name="format--fixed-width"></a>格式 = 固定宽度  
 **字体**  
 选择用于显示预览数据的字体。  
  
 **源数据列**  
 通过滑动垂直的行标记可以调整行宽，通过单击预览窗口顶部的标尺可以调整列宽  
  
 **行宽**  
 为各列添加分隔符之前，先指定行的长度。 或者，拖动预览窗口中的垂直线，以标记行尾。 行宽值将自动更新。  
  
 **重置列**  
 通过单击“重置列”可以删除除原始列之外的所有列。  
  
#### <a name="format--ragged-right"></a>格式 = 右边未对齐  
  
> [!NOTE]  
>  右边未对齐是指文件中除最后一列之外每一列的宽度都固定。 它由行分隔符分隔。  
  
 **字体**  
 选择用于显示预览数据的字体。  
  
 **源数据列**  
 通过滑动垂直的行标记可以调整行宽，通过单击预览窗口顶部的标尺可以调整列宽  
  
 **行分隔符**  
 从可用行分隔符的列表中选择，或输入分隔符文本。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**{CR}{LF}**|行由回车符和换行符的组合分隔。|  
|**{CR}**|行由回车符分隔。|  
|**{LF}**|行由换行符分隔。|  
|**分号 {;}**|行由分号分隔。|  
|**冒号 {:}**|行由冒号分隔。|  
|**逗号 {,}**|行由逗号分隔。|  
|**制表符 {t}**|行由制表符分隔。|  
|**竖线 {|}**。|行由竖线分隔。|  
  
 **重置列**  
 通过单击“重置列”可以删除除原始列之外的所有列。  
  
## <a name="multiple-flat-files-connection-manager-editor-advanced-page"></a>多平面文件连接管理器编辑器（“高级”页）
  可以使用“多平面文件连接管理器编辑器”对话框的“高级”页，设置平面文件连接管理器连接到的文本文件中的属性（如每列的数据类型和分隔符）。  
  
 默认情况下，字符串列的长度为 50 个字符。 您可以计算示例数据并自动调整这些列的长度，以免数据截断或超出列宽。 还可以更新其他元数据以便与目标列兼容。 例如，可以将只包含整型数据的列的数据类型更改为数值数据类型，例如 DT_I2。  
  
 若要了解有关多平面文件连接管理器的详细信息，请参阅 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)。  
  
### <a name="options"></a>选项  
 **连接管理器名称**  
 为工作流中的多平面文件连接管理器提供一个唯一名称。 所提供的名称将显示在 **设计器的** “连接管理器” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 区域中。  
  
 **Description**  
 描述连接管理器。 最好按照连接管理器的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
 **配置各列的属性**  
 选择左窗格中的列可在右窗格中查看列的属性。 请参阅下表以了解数据类型属性的说明。 列出的部分属性仅对某些平面文件格式是可配置的。  
  
|属性|描述|  
|--------------|-----------------|  
|**ColumnType**|表示列是由分隔符分隔、还是固定宽度，或是右边未对齐。 该属性为只读。 在右边未对齐的文件中，除最后一列之外的每一列的宽度都固定，而最后一列由行分隔符终止。|  
|**OutputColumnWidth**|指定值以字节数进行存储；对于 Unicode 文件，该值将显示为字符数。 在数据流任务中，此值用于设置平面文件源的输出列宽。<br /><br /> 注意：在对象模型中，此属性的名称为 MaximumWidth。|  
|**DataType**|从可用数据类型的列表中进行选择。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。|  
|**TextQualified**|指示是否使用文本限定符限定文本数据：<br /><br /> **True**：平面文件中的文本数据是受限定的。<br /><br /> **False**：平面文件中的文本数据是不受限定的。|  
|**名称**|提供列名。 默认为带编号的列列表，不过，您也可以任选一个唯一的描述性名称。|  
|**DataScale**|指定数字数据的小数位数。 小数位数是指小数点后的位数。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。|  
|**ColumnDelimiter**|从可用列分隔符的列表中进行选择。 选择不可能出现在文本中的分隔符。 对于固定宽度的列，将忽略此值。<br /><br /> **{CR}{LF}** - 列由回车符和换行符的组合分隔<br /><br /> **{CR}** - 列由回车符分隔<br /><br /> **{LF}** - 列由换行符分隔<br /><br /> **分号 {;}** - 列由分号分隔<br /><br /> **冒号 {:}** - 列由冒号分隔<br /><br /> **逗号 {,}** - 列由逗号分隔<br /><br /> **制表符 {t}** - 列由制表符分隔<br /><br /> **竖线 {&#124;}** - 列由竖线分隔|  
|**DataPrecision**|指定数字数据的精度。 精度是指数字的位数。 有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。|  
|**InputColumnWidth**|指定值以字节数进行存储；对于 Unicode 文件，该值将显示为字符数。 对于分隔列，将忽略此值。<br /><br /> **注意** ：在对象模型中，此属性的名称为 ColumnWidth。|  
  
 **新建**  
 单击“新建”添加一个新列。 默认情况下，单击 **“新建”** 按钮将会在列表末尾添加新列。 该按钮还包括以下选项，可以在下拉列表中选择。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**添加列**|在列表末尾添加新列。|  
|**在其前插入**|在所选列前面插入新列。|  
|**在其后插入**|在所选列后面插入新列。|  
  
 **删除**  
 选择一列，然后单击“删除”来删除该列。  
  
 **建议类型**  
 使用“提供列类型建议”对话框可以评估所选的第一个文件中的示例数据，并获取对每列的数据类型和长度的建议。 有关详细信息，请参阅 [“提供列类型建议”对话框 UI 参考](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md)。  
  
## <a name="multiple-flat-files-connection-manager-editor-preview-page"></a>多平面文件连接管理器编辑器（“预览”页）
  可以使用“多平面文件连接管理器编辑器”对话框的“预览”页，查看选择的第一个源文件在按定义的样式划分为多列后的显示情况。  
  
 若要了解有关多平面文件连接管理器的详细信息，请参阅 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)。  
  
### <a name="options"></a>选项  
 **连接管理器名称**  
 为工作流中的“多平面文件连接”提供一个唯一名称。 所提供的名称将显示在 **设计器的** “连接管理器” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 区域中。  
  
 **Description**  
 描述此连接。 最好按照连接的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
 **要跳过的数据行数**  
 指定在平面文件的开头要跳过多少行。  
  
 **预览行**  
 查看所选择的第一个平面文件中的示例数据，这些数据已按所选的选项划分为列和行。  
  
## <a name="see-also"></a>另请参阅  
 [“平面文件源”](../../integration-services/data-flow/flat-file-source.md)   
 [平面文件目标](../../integration-services/data-flow/flat-file-destination.md)   
 [Integration Services (SSIS) 连接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
