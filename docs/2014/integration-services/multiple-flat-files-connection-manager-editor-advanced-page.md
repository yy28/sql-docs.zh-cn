---
title: 多平面文件连接管理器编辑器 （高级页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multifile.advanced.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: fc883131-c03d-4ab3-8220-b51cbe243a82
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dda5cb294536354ed4bcc5003983d36f61167007
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48143327"
---
# <a name="multiple-flat-files-connection-manager-editor-advanced-page"></a>多平面文件连接管理器编辑器（“高级”页）
  可以使用“多平面文件连接管理器编辑器”对话框的“高级”页，设置平面文件连接管理器连接到的文本文件中的属性（如每列的数据类型和分隔符）。  
  
 默认情况下，字符串列的长度为 50 个字符。 您可以计算示例数据并自动调整这些列的长度，以免数据截断或超出列宽。 还可以更新其他元数据以便与目标列兼容。 例如，可以将只包含整型数据的列的数据类型更改为数值数据类型，例如 DT_I2。  
  
 若要了解有关多平面文件连接管理器的详细信息，请参阅 [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md)。  
  
## <a name="options"></a>选项  
 **连接管理器名称**  
 为工作流中的多平面文件连接管理器提供一个唯一名称。 所提供的名称将显示在 **设计器的** “连接管理器” [!INCLUDE[ssIS](../includes/ssis-md.md)] 区域中。  
  
 **Description**  
 描述连接管理器。 最好按照连接管理器的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
 **配置各列的属性**  
 选择左窗格中的列可在右窗格中查看列的属性。 请参阅下表以了解数据类型属性的说明。 列出的部分属性仅对某些平面文件格式是可配置的。  
  
|“属性”|Description|  
|--------------|-----------------|  
|**ColumnType**|表示列是由分隔符分隔、还是固定宽度，或是右边未对齐。 该属性为只读。 在右边未对齐的文件中，除最后一列之外的每一列的宽度都固定，而最后一列由行分隔符终止。|  
|**OutputColumnWidth**|指定值以字节数进行存储；对于 Unicode 文件，该值将显示为字符数。 在数据流任务中，此值用于设置平面文件源的输出列宽。<br /><br /> 注意：在对象模型中，此属性的名称为 MaximumWidth。|  
|**DataType**|从可用数据类型的列表中进行选择。 有关详细信息，请参阅 [Integration Services 数据类型](data-flow/integration-services-data-types.md)。|  
|**TextQualified**|指示是否使用文本限定符限定文本数据。 有效值为<br /><br /> **True**：平面文件中的文本数据是受限定的。<br /><br /> **False**：平面文件中的文本数据是不受限定的。|  
|**名称**|提供列名。 默认为带编号的列列表，不过，您也可以任选一个唯一的描述性名称。|  
|**DataScale**|指定数字数据的小数位数。 小数位数是指小数点后的位数。 有关详细信息，请参阅 [Integration Services 数据类型](data-flow/integration-services-data-types.md)。|  
|**ColumnDelimiter**|从可用列分隔符的列表中进行选择。 选择不可能出现在文本中的分隔符。 对于固定宽度的列，将忽略此值。<br /><br /> **{CR}{LF}** – 列由回车符和换行符的组合分隔<br /><br /> **{CR}** – 列由回车符分隔<br /><br /> **{LF}** – 列由换行符分隔<br /><br /> **分号 {;}** – 列由分号分隔<br /><br /> **冒号 {:}** – 列由冒号分隔<br /><br /> **逗号 {,}** - 列由逗号分隔<br /><br /> **制表符 {t}** – 列由制表符分隔<br /><br /> **竖线 {&#124;}** – 列由竖线分隔|  
|**DataPrecision**|指定数字数据的精度。 精度是指数字的位数。 有关详细信息，请参阅 [Integration Services 数据类型](data-flow/integration-services-data-types.md)。|  
|**InputColumnWidth**|指定值以字节数进行存储；对于 Unicode 文件，该值将显示为字符数。 对于分隔列，将忽略此值。<br /><br /> **注意** ：在对象模型中，此属性的名称为 ColumnWidth。|  
  
 **新建**  
 单击“新建”添加一个新列。 默认情况下，单击 **“新建”** 按钮将会在列表末尾添加新列。 该按钮还包括以下选项，可以在下拉列表中选择。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**添加列**|在列表末尾添加新列。|  
|**在其前插入**|在所选列前面插入新列。|  
|**在其后插入**|在所选列后面插入新列。|  
  
 **删除**  
 选择一列，然后单击“删除”来删除该列。  
  
 **建议类型**  
 使用“提供列类型建议”对话框可以评估所选的第一个文件中的示例数据，并获取对每列的数据类型和长度的建议。 有关详细信息，请参阅[“提供列类型建议”对话框 UI 参考](connection-manager/suggest-column-types-dialog-box-ui-reference.md)。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [多平面文件连接管理器编辑器&#40;常规页&#41;](general-page-of-integration-services-designers-options.md)   
 [多平面文件连接管理器编辑器&#40;列页&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [多平面文件连接管理器编辑器&#40;预览页&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  
