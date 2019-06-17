---
title: 连接到平面文件数据源（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d7e7067b-f5a5-482f-b97e-9d82fe8e9f76
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e1c2789d8d10928bcbe576fc57f630675fdbd405
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65723899"
---
# <a name="connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard"></a>连接到平面文件数据源（SQL Server 导入和导出向导）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本主题介绍如何从 SQL Server 导入和导出向导的“选择数据源”或“选择目标”页连接到平面文件（文本文件）数据源    。 对于平面文件，向导的这两页显示的选项集不同，所以本主题会分别介绍平面文件源和平面文件目标。

## <a name="an-alternative-for-simple-text-import"></a>简单文本导入的替代方法
如果必须将文本文件导入 SQL Server 且无需导入和导出向导中提供的所有配置选项，可考虑使用 SQL Server Management Studio (SSMS) 中的“导入平面文件向导”  。 有关详细信息，请参阅下文：
- [SQL Server Management Studio 17.3 中的新增功能](https://blogs.technet.microsoft.com/dataplatforminsider/2017/10/10/whats-new-in-sql-server-management-studio-17-3/)
- [SSMS 17.3 中的新导入平面文件向导简介](https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173)

## <a name="connect-to-a-flat-file-source"></a>连接到平面文件源
 
 平面文件数据源的选项共有四页。 页数挺多！ 但无需在每页上花太多时间。 以下是要考虑的内容。
 
第|建议  |类型  
----|---------|---------
**常规**|请确保更新“格式”  部分中的选项。|建议    
**“列”**|请确保检查列和行分隔符（适用于带分隔符的文件）或标记列（适用于宽度固定的文件）。|建议
**高级**|（可选）检查默认分配到列的数据类型和其他属性。|可选
**预览**|（可选）预览一个使用指定设置的示例数据。|可选

## <a name="general-page-source"></a>常规页（源）
 在“常规”  页上，浏览以选择文件，然后验证“格式”  部分中的设置。
 
 ![平面文件连接 常规](../../integration-services/import-export-data/media/flat-file-connection-general.png)  

### <a name="options-to-specify-general-page"></a>要指定的选项（“常规”  页）

 **文件名**  
 输入平面文件的路径和文件名。  
  
 **“浏览”**  
 查找平面文件。  
  
 **区域设置**  
 指定区域设置，以便为排序以及日期和事件格式提供语言特定的信息。  
  
 **Unicode**  
 指定文件是否使用 Unicode。 如果使用 Unicode，则不能指定代码页。  
  
 **代码页**  
 指定非 Unicode 文本的代码页。  
  
 **格式**  
 选择文件是使用带分隔符、固定宽度还是右边不对齐的格式。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|带分隔符|列由分隔符分隔。 在“列”  页上指定分隔符。|  
|固定宽度|列的宽度固定。|  
|右边未对齐|在右边未对齐的文件中，除最后一列之外的每一列的宽度都固定，而最后一列由行分隔符进行分隔。|  
  
 **文本限定符**  
 指定供文件使用的文本限定符（若存在）。 例如，可以指定文本字段必须用引号括起来。 （此属性仅适用于带分隔符的文件。） 
  
> [!NOTE]
> 选择文本限定符之后，不能重新选择“无”  选项。 键入 **None** 以取消选择文本限定符。  
  
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
|**竖线 {&#124;}** 。|标题行由竖线分隔。|  
  
 **要跳过的标题行数**  
 指定要在文件顶部跳过的行数（若存在）。  
  
 **第一个数据行中的列名称**  
 指定第一行（任何跳过的行之后）是否包含列名称。

## <a name="columns-page---format--delimited-source"></a>列页 — 格式 = 带分隔符（源）
 在“列”  页上，验证列列表以及向导已标识的分隔符。 以下屏幕截图显示将“带分隔符”  选作平面文件格式时的页面。
 
![平面文件、带分隔符、“列”页](../../integration-services/import-export-data/media/flat-file-delimited-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--delimited"></a>要指定的选项（“列”  页 — 格式 = 带分隔符）

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
|**竖线 {&#124;}** 。|行由竖线分隔。|  
  
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
|**竖线 {&#124;}** 。|列由竖线分隔。|  
  
 **预览行**  
 查看平面文件中的示例数据，这些数据已按所选的选项划分为列和行。  
 
 **“刷新”**  
 通过单击“刷新”  查看更改要跳过的分隔符后的效果。 只有在更改其他连接选项之后，此按钮才可见。  
  
 **重置列**  
 还原原始列。  

## <a name="columns-page---format--fixed-width-source"></a>“列”页 — 格式 = 固定宽度（源）
在“列”  页上，验证列列表以及向导已标识的分隔符。 以下屏幕截图显示将“固定宽度”  选作平面文件格式时的页面。
  
![平面文件、固定宽度、“列”页](../../integration-services/import-export-data/media/flat-file-fixed-width-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--fixed-width"></a>要指定的选项（“列”  页 — 格式 = 固定宽度）

 **字体**  
 选择用于显示预览数据的字体。  
  
 **源数据列**  
 通过滑动垂直的红色行标记可以调整行宽，通过单击预览窗口顶部的标尺可以调整列宽。  
  
 **行宽**  
 为各列添加分隔符之前，先指定行的长度。 或者，拖动预览窗口中的垂直红线，以标记行尾。 行宽值将自动更新。  
  
 **重置列**  
 还原原始列。  
  
## <a name="columns-page---format--ragged-right-source"></a>“列”页 - 格式 = 右边不对齐（源）
在“列”  页上，验证列列表以及向导已标识的分隔符。 以下屏幕截图显示将“右边不对齐”  选作平面文件格式时的页面。

> [!NOTE]
> 在右边未对齐的文件中，除最后一列之外的每一列的宽度都固定，而最后一列由行分隔符进行分隔。  
 
![平面文件、右边不对齐、“列”页](../../integration-services/import-export-data/media/flat-file-ragged-right-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--ragged-right"></a>要指定的选项（“列”  页 — 格式 = 右边不对齐）
   
 **字体**  
 选择用于显示预览数据的字体。  
  
 **源数据列**  
 通过滑动垂直的红色行标记可以调整行宽，通过单击预览窗口顶部的标尺可以调整列宽。  
  
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
|**竖线 {&#124;}** 。|行由竖线分隔。|  
  
 **重置列**  
 还原原始列。  

## <a name="advanced-page-source"></a>“高级”页（源）
“高级”  页显示有关数据源中每个列的详细信息，包括其数据类型和大小。 以下屏幕截图显示带分隔符的平面文件中第一列的“高级”  页。

![平面文件、带分隔符、“高级”页](../../integration-services/import-export-data/media/flat-file-delimited-advanced-page.jpg)

请注意，在屏幕截图中，包含数字的 ID  列最初的数据类型为字符串。

### <a name="options-to-specify-advanced-page"></a>要指定的选项（“高级”  页）

 **配置各列的属性**  
 选择左窗格中的列可在右窗格中查看列的属性。 请参阅下表，获取有关列属性的说明。 所列出的某些属性仅可针对特定平面文件格式和特定数据类型的列进行配置。  
  
|属性|描述|  
|--------------|-----------------|  
|**名称**|提供说明性列名。 如果不输入名称，则 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将自动创建名称，格式为列 0、列 1，依此类推。|
|**ColumnDelimiter**|从可用列分隔符的列表中进行选择。 选择不可能出现在文本中的分隔符。 对于固定宽度的列，将忽略此值。<br /><br /> **{CR}{LF}** 。 列由回车符和换行符的组合分隔。<br /><br /> **{CR}** 。 列由回车符分隔。<br /><br /> **{LF}** 。 列由换行符分隔。<br /><br /> **分号 {;}** 。 列由分号分隔。<br /><br /> **冒号 {:}** 。 列由冒号分隔。<br /><br /> **逗号 {,}** 。 列由逗号分隔。<br /><br /> **制表符 {t}** 。 列由制表符分隔。<br /><br /> **竖线 {&#124;}** 。 列由竖线分隔。|
|**ColumnType**|表示列是由分隔符分隔、还是固定宽度，或是右边未对齐。 该属性为只读。 在右边未对齐的文件中，除最后一列之外的每一列的宽度都固定。 它由行分隔符分隔。|  
|**InputColumnWidth**|指定值存储为字节数；对于 Unicode 文件，此值为字符数。 对于分隔列，将忽略此值。<br /><br /> **注意** ：在对象模型中，此属性的名称为 ColumnWidth。|
|**DataPrecision**|指定数字数据的精度。 精度是指数字的位数。|
|**DataScale**|指定数字数据的小数位数。 小数位数是指小数点后的位数。|
|**DataType**|从可用数据类型的列表中进行选择。<br/>有关详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。|
|**OutputColumnWidth**|指定值存储为字节数；对于 Unicode 文件，此值对应于字符数。 在数据流任务中，此值用于设置平面文件源的输出列宽。 在对象模型中，此属性的名称为 MaximumWidth。|  
|**TextQualified**|指示文本数据周围是否有文本限定符（例如引号字符）。<br /><br /> True：平面文件中的文本数据是受限定的。 False：平面文件中的文本数据是不受限定的。|  
  
**新建**  
 单击“新建”  添加一个新列。 默认情况下，单击 **“新建”** 按钮将会在列表末尾添加新列。 该按钮还包括以下选项，可以在下拉列表中选择。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**添加列**|在列表末尾添加新列。|  
|**在其前插入**|在所选列前面插入新列。|  
|**在其后插入**|在所选列后面插入新列。|  
  
 **删除**  
 选择一列，然后单击“删除”  来删除该列。  
  
 **建议类型**  
 使用  “提供列类型建议”对话框可以计算文件中的示例数据，并获取关于每列的数据类型和长度的建议。  
 
单击“建议类型”  可显示“提供列类型建议”  对话框。 

![平面文件连接建议类型对话框](../../integration-services/import-export-data/media/flat-file-connection-suggest.png)

在选择“建议列类型”对话框中的选项并单击“确定”之后，向导可能会更改某些列的数据类型   。

下面的屏幕截图显示，单击“建议类型”之后，向导已识别出数据源中的“ID”列实际上是数字而不是文本字符串，并且向导已将该列的数据类型从字符串更改为整数   。

![平面文件连接 高级 之后](../../integration-services/import-export-data/media/flat-file-connection-advanced-after.png)

有关详细信息，请参阅[“提供列类型建议”对话框 UI 参考](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md)。

## <a name="preview-page-source"></a>“预览”页（源）

在“预览”  页上，验证列列表和示例数据是否符合你的预期。

![平面文件、“预览”页](../../integration-services/import-export-data/media/flat-file-preview-page.jpg)

### <a name="options-to-specify-preview-page"></a>要指定的选项（“预览”  页）

 **要跳过的数据行数**  
 指定在平面文件的开头要跳过多少行。  
  
 **预览行**  
 查看平面文件中的示例数据，这些数据已按所选的选项划分为列和行。
 
 **“刷新”**  
 通过单击“刷新”可以查看更改要跳过的行数后的效果。  只有在更改其他连接选项之后，此按钮才可见。  
 
有关“预览”  页的详细信息，请参阅以下 Integration Services 参考页面：[平面文件连接管理器编辑器（“预览”页）](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)。

## <a name="connect-to-a-flat-file-destination"></a>连接到平面文件目标
对于平面文件目标，只有一页选项，如以下屏幕截图所示。 浏览以选择文件，然后在“格式”  部分验证设置。

![连接到平面文件目标](../../integration-services/import-export-data/media/connect-to-flat-file-destination.jpg)

### <a name="options-to-specify-choose-a-destination-page"></a>要指定的选项（“选择目标”  页）

 **文件名**  
 输入平面文件的路径和文件名。  
  
 **“浏览”**  
 查找平面文件。  
  
 **区域设置**  
 指定区域设置，以便为排序以及日期和事件格式提供语言特定的信息。  
  
 **Unicode**  
 指定文件是否使用 Unicode。 如果使用 Unicode，则不能指定代码页。  
  
 **代码页**  
 指定非 Unicode 文本的代码页。  
  
 **格式**  
 选择文件是使用带分隔符、固定宽度还是右边不对齐的格式。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|带分隔符|列由分隔符分隔。 在“列”  页上指定分隔符。|  
|固定宽度|列的宽度固定。|  
|右边未对齐|在右边未对齐的文件中，除最后一列之外的每一列的宽度都固定，而最后一列由行分隔符进行分隔。|  
  
 **文本限定符**  
 指定供文件使用的文本限定符（若存在）。 例如，可以指定文本字段必须用引号括起来。 （此属性仅适用于带分隔符的文件。） 
  
> [!NOTE] 
> 选择文本限定符之后，不能重新选择“无”  选项。 键入 **None** 以取消选择文本限定符。  

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

