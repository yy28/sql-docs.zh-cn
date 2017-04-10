---
title: "平面文件连接管理器编辑器（“高级”页） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.ffileconnection.columnproperties.f1"
helpviewer_keywords: 
  - "平面文件连接管理器编辑器"
ms.assetid: 58aa3dee-4774-4e0b-a956-96d199be4c3a
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 36
---
# 平面文件连接管理器编辑器（“高级”页）
  可以使用 **“平面文件连接管理器编辑器”** 对话框的 **“高级”** 页，设置指定 Integration Services 如何读写平面文件中的数据的属性。 可以更改平面文件中各个列的名称，并设置包括文件中每个列的数据类型和分隔符在内的属性。  
  
 默认情况下，字符串列的长度为 50 个字符。 可以调整这些列的长度，以免数据截断或超出列宽。 还可以更新其他元数据以便与目标列兼容。 例如，可以将只包含整型数据的列的数据类型更改为数值数据类型，例如 DT_I2。 可以手动进行这些修改，也可以单击 **“选择类型”** 按钮，以使用 **“提供列类型建议”** 对话框来评估示例数据并自动进行其中一些更改。  
  
 若要了解有关平面文件连接管理器的详细信息，请参阅 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)。  
  
## 选项  
 **连接管理器名称**  
 为工作流中的平面文件连接管理器提供唯一的名称。 所提供的名称将在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中显示。  
  
 **Description**  
 描述连接管理器。 最好按照连接管理器的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
 **配置各列的属性**  
 选择左窗格中的列可在右窗格中查看列的属性。 请参阅下表以了解数据类型属性的说明。 列出的部分属性仅对某些平面文件格式是可配置的。  
  
|属性|Description|  
|--------------|-----------------|  
|**ColumnType**|表示列是由分隔符分隔、还是固定宽度，或是右边未对齐。 该属性为只读。 在右边未对齐的文件中，除最后一列之外的每一列的宽度都固定。 它由行分隔符分隔。|  
|**OutputColumnWidth**|指定值存储为字节数；对于 Unicode 文件，此值对应于字符数。 在数据流任务中，此值用于设置平面文件源的输出列宽。 在对象模型中，此属性的名称为 MaximumWidth。|  
|**DataType**|从可用数据类型的列表中进行选择。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。|  
|**TextQualified**|指示文本数据周围是否有文本限定符（例如引号字符）。<br /><br /> True：平面文件中的文本数据是受限定的。 False：平面文件中的文本数据是不受限定的。|  
|**名称**|提供说明性列名。 如果不输入名称，则 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将自动创建名称，格式为“列 0”、“列 1”，依此类推。|  
|**DataScale**|指定数字数据的小数位数。 小数位数是指小数点后的位数。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。|  
|**ColumnDelimiter**|从可用列分隔符的列表中进行选择。 选择不可能出现在文本中的分隔符。 对于固定宽度的列，将忽略此值。<br /><br /> **{CR}{LF}**。 列由回车符和换行符的组合分隔。<br /><br /> **{CR}**。 列由回车符分隔。<br /><br /> **{LF}**。 列由换行符分隔。<br /><br /> **分号 {;}**。 列由分号分隔。<br /><br /> **冒号 {:}**。 列由冒号分隔。<br /><br /> **逗号 {,}**。 列由逗号分隔。<br /><br /> **制表符 {t}**。 列由制表符分隔。<br /><br /> **竖线 {|}**。 列由竖线分隔。|  
|**DataPrecision**|指定数字数据的精度。 精度是指数字的位数。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。|  
|**InputColumnWidth**|指定值以字节数进行存储；对于 Unicode 文件，该值将显示为字符数。 对于分隔列，将忽略此值。<br /><br /> **注意**：在对象模型中，此属性的名称为 ColumnWidth。|  
  
 **新建**  
 单击“新建”添加一个新列。 默认情况下，单击 **“新建”** 按钮将会在列表末尾添加新列。 该按钮还包括以下选项，可以在下拉列表中选择。  
  
|“值”|Description|  
|-----------|-----------------|  
|**添加列**|在列表末尾添加新列。|  
|**在其前插入**|在所选列前面插入新列。|  
|**在其后插入**|在所选列后面插入新列。|  
  
 **删除**  
 选择一列，然后单击“删除”来删除该列。  
  
 **建议类型**  
 使用“提供列类型建议”对话框可以计算文件中的示例数据，并获取关于每列的数据类型和长度的建议。 有关详细信息，请参阅[“提供列类型建议”对话框 UI 参考](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md)。  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [平面文件连接管理器编辑器（“常规”页）](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)   
 [平面文件连接管理器编辑器（“列”页）](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)   
 [平面文件连接管理器编辑器（“预览”页）](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)  
  
  