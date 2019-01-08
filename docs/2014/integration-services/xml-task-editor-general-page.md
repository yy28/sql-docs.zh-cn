---
title: XML 任务编辑器 （常规页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmltask.general.f1
helpviewer_keywords:
- XML Task Editor
ms.assetid: b9622c48-3243-4408-a1de-9ba20e32ff70
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 49c05c47492913c02df6591f78e1deea531de809
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377908"
---
# <a name="xml-task-editor-general-page"></a>XML 任务编辑器（“常规”页）
  可以使用 **“XML 任务编辑器”** 对话框的 **“常规节点”** ，指定操作类型以及配置操作。  
  
 若要了解此任务，请参阅 [XML Task](control-flow/xml-task.md)。 有关使用 XML 文档和数据的信息，请参阅 MSDN Library 中的“[Employing XML in the .NET Framework](https://go.microsoft.com/fwlink/?LinkId=56214)”。  
  
## <a name="static-options"></a>静态选项  
 **OperationType**  
 从列表中选择操作类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**验证**|根据文档类型定义 (DTD) 或 XML 架构定义 (XSD) 架构验证 XML 文档。 选择此选项将在 **Validate**部分中显示动态选项。|  
|**XSLT**|对 XML 文档执行 XSL 转换。 选择此选项将在 **XSLT**部分中显示动态选项。|  
|**XPATH**|执行 XPath 查询和计算。 选择此选项将在 **XPATH**部分中显示动态选项。|  
|**合并**|合并两个 XML 文档。 选择此选项将在 **Merge**部分中显示动态选项。|  
|**差异**|比较两个 XML 文档。 选择此选项将在 **Diff**部分中显示动态选项。|  
|**Patch**|应用 Diff 运算的输出以创建新文档。 选择此选项将在 **Patch**部分中显示动态选项。|  
  
 **SourceType**  
 选择 XML 文档的源类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为 XML 文档。|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **数据源**  
 如果将“源”设置为“直接输入”，请提供 XML 代码，或单击省略号按钮 (…)，再使用“文档源编辑器”对话框提供 XML 代码。  
  
 如果将“源”设置为“文件连接”，请选择文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将“源”设置为“变量”，请选择现有变量，或单击“\<新建变量...>”，创建新的变量。  
  
 **相关主题**:[Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)，[添加变量](../../2014/integration-services/add-variable.md)。  
  
## <a name="operationtype-dynamic-options"></a>OperationType 动态选项  
  
### <a name="operationtype--validate"></a>OperationType = Validate  
 指定验证操作的选项。  
  
 **SaveOperationResult**  
 指定 XML 任务是否保存验证操作的输出。  
  
 **OverwriteDestination**  
 指定是否覆盖目标文件或变量。  
  
 **目标**  
 选择现有文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **目标类型**  
 选择 XML 文档的目标类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **ValidationType**  
 选择验证类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**DTD**|使用文档类型定义 (DTD)。|  
|**XSD**|使用 XML 架构定义 (XSD) 架构。 选择此选项将在 **ValidationType**部分中显示动态选项。|  
  
 **FailOnValidationFail**  
 指定在文档验证失败时操作是否失败。  
  
 **ValidationDetails**  
 当此属性的值为 true 时会提供大量错误输出。 有关详细信息，请参阅 [Validate XML with the XML Task](control-flow/validate-xml-with-the-xml-task.md)。  
  
### <a name="validationtype-dynamic-options"></a>ValidationType 动态选项  
  
#### <a name="validationtype--xsd"></a>ValidationType = XSD  
 **SecondOperandType**  
 选择第二个 XML 文档的源类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为 XML 文档。|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **SecondOperand**  
 如果将“SecondOperandType”设置为“直接输入”，请提供 XML 代码，或单击省略号按钮 (…)，再使用“源编辑器”对话框提供 XML 代码。  
  
 如果将“SecondOperandType”设置为“文件连接”，请选择文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将“XPathStringSourceType”设置为“变量”，请选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题**:[Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)，[添加变量](../../2014/integration-services/add-variable.md)。  
  
### <a name="operationtype--xslt"></a>OperationType = XSLT  
 指定 XSLT 操作的选项。  
  
 **SaveOperationResult**  
 指定 XML 任务是否保存 XSLT 操作的输出。  
  
 **OverwriteDestination**  
 指定是否覆盖目标文件或变量。  
  
 **目标**  
 如果将“DestinationType”设置为“文件连接”，请选择文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将“DestinationType”设置为“变量”，请选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题**:[Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)，[添加变量](../../2014/integration-services/add-variable.md)。  
  
 **目标类型**  
 选择 XML 文档的目标类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **SecondOperandType**  
 选择第二个 XML 文档的源类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为 XML 文档。|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **SecondOperand**  
 如果将“SecondOperandType”设置为“直接输入”，请提供 XML 代码，或单击省略号按钮 (…)，再使用“源编辑器”对话框提供 XML 代码。  
  
 如果将“SecondOperandType”设置为“文件连接”，请选择文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将“XPathStringSourceType”设置为“变量”，请选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题**:[Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)，[添加变量](../../2014/integration-services/add-variable.md)。  
  
### <a name="operationtype--xpath"></a>OperationType = XPATH  
 指定 XPath 操作的选项。  
  
 **SaveOperationResult**  
 指定 XML 任务是否保存 XPath 操作的输出。  
  
 **OverwriteDestination**  
 指定是否覆盖目标文件或变量。  
  
 **目标**  
 如果将“DestinationType”设置为“文件连接”，请选择文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将“DestinationType”设置为“变量”，请选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题**:[Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)，[添加变量](../../2014/integration-services/add-variable.md)。  
  
 **目标类型**  
 选择 XML 文档的目标类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **SecondOperandType**  
 选择第二个 XML 文档的源类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为 XML 文档。|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **SecondOperand**  
 如果将“SecondOperandType”设置为“直接输入”，请提供 XML 代码，或单击省略号按钮 (…)，再使用“源编辑器”对话框提供 XML 代码。  
  
 如果将“SecondOperandType”设置为“文件连接”，请选择文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将“XPathStringSourceType”设置为“变量”，请选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题**:[Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)，[添加变量](../../2014/integration-services/add-variable.md)。  
  
 **PutResultInOneNode**  
 指定是否将结果写入单个节点。  
  
 **XPathOperation**  
 选择 XPath 结果类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**Evaluation**|返回 XPath 函数的结果。|  
|**Node list**|将所选节点返回为 XML 片段。|  
|**值**|返回所有所选节点的内部文本值，将其连接为字符串。|  
  
### <a name="operationtype--merge"></a>OperationType = Merge  
 指定合并操作的选项。  
  
 **XPathStringSourceType**  
 选择 XML 文档的源类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为 XML 文档。|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **XPathStringSource**  
 如果将“XPathStringSourceType”设置为“直接输入”，请提供 XML 代码，或单击省略号按钮 (…)，再使用“文档源编辑器”对话框提供 XML 代码。  
  
 如果将“XPathStringSourceType”设置为“文件连接”，请选择文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将“XPathStringSourceType”设置为“变量”，请选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题**:[Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)，[添加变量](../../2014/integration-services/add-variable.md)  
  
 使用 XPath 语句标识源文档中的合并位置时，此语句应返回一个节点。 如果该语句返回多个节点，则仅使用第一个节点。 第二个文档的内容在 XPath 查询返回的第一个节点下合并。  
  
 **SaveOperationResult**  
 指定 XML 任务是否保存合并操作的输出。  
  
 **OverwriteDestination**  
 指定是否覆盖目标文件或变量。  
  
 **目标**  
 如果将“DestinationType”设置为“文件连接”，请选择文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将“DestinationType”设置为“变量”，请选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题**:[Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)，[添加变量](../../2014/integration-services/add-variable.md)。  
  
 **目标类型**  
 选择 XML 文档的目标类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **SecondOperandType**  
 选择第二个 XML 文档的目标类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为 XML 文档。|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **SecondOperand**  
 如果将“SecondOperandType”设置为“直接输入”，请提供 XML 代码，或单击省略号按钮 (…)，再使用“文档源编辑器”对话框提供 XML 代码。  
  
 如果将“SecondOperandType”设置为“文件连接”，请选择文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将“SecondOperandType”设置为“变量”，请选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题**:[Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)，[添加变量](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--diff"></a>OperationType = Diff  
 指定 Diff 运算的选项。  
  
 **DiffAlgorithm**  
 选择在比较文档时要使用的 Diff 算法。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**Auto**|由 XML 任务确定是使用快速算法还是使用精确算法。|  
|**Fast**|使用快速但精确度较低的 Diff 算法。|  
|**Precise**|使用精确的 Diff 算法。|  
  
 **Diff 选项**  
 将 Diff 选项设置为应用于 Diff 运算。 下表中列出了这些选项：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**IgnoreXMLDeclaration**|指定是否比较 XML 声明。|  
|**IgnoreDTD**|指定是否忽略文档类型定义 (DTD)。|  
|**IgnoreWhite Spaces**|指定比较文档时是否忽略空格数量的不同。|  
|**IgnoreNamespaces**|指定是否比较元素及其属性名称的命名空间统一资源标识符 (URI)。<br /><br /> 注意：如果将此选项设置为 `True`，则本地名称相同但命名空间不同的两个元素将被视为同一元素。|  
|**IgnoreProcessingInstructions**|指定是否比较处理指令。|  
|**IgnoreOrderOf ChildElements**|指定是否比较子元素的顺序。<br /><br /> 注意：如果将此选项设置为 `True`，同级列表中仅位置不同的子元素将被视为同一子元素。|  
|**IgnoreComments**|指定是否比较注释节点。|  
|**IgnorePrefixes**|指定是否比较元素及属性名称的前缀。<br /><br /> 注意：如果将此选项设置为 `True`，则本地名称相同但命名空间 URI 和前缀不同的两个元素将被视为同一元素。|  
  
 **FailOnDifference**  
 指定在 Diff 运算失败时任务是否失败。  
  
 **SaveDiffGram**  
 指定是否保存比较结果，即 DiffGram 文档。  
  
 **SaveOperationResult**  
 指定 XML 任务是否保存 Diff 运算的输出。  
  
 **OverwriteDestination**  
 指定是否覆盖目标文件或变量。  
  
 **目标**  
 如果将“DestinationType”设置为“文件连接”，请选择文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将“DestinationType”设置为“变量”，请选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题**:[Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)，[添加变量](../../2014/integration-services/add-variable.md)。  
  
 **目标类型**  
 选择 XML 文档的目标类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **SecondOperandType**  
 选择 XML 文档的目标类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为 XML 文档。|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **SecondOperand**  
 如果将“SecondOperandType”设置为“直接输入”，请提供 XML 代码，或单击省略号按钮 (…)，再使用“文档源编辑器”对话框提供 XML 代码。  
  
 如果将“SecondOperandType”设置为“文件连接”，请选择文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将“SecondOperandType”设置为“变量”，请选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题**:[Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)，[添加变量](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--patch"></a>OperationType = Patch  
 指定修补操作的选项。  
  
 **SaveOperationResult**  
 指定 XML 任务是否保存修补操作的输出。  
  
 **OverwriteDestination**  
 指定是否覆盖目标文件或变量。  
  
 **目标**  
 如果将“DestinationType”设置为“文件连接”，请选择文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将“DestinationType”设置为“变量”，请选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题**:[Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)，[添加变量](../../2014/integration-services/add-variable.md)。  
  
 **目标类型**  
 选择 XML 文档的目标类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **SecondOperandType**  
 选择 XML 文档的目标类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为 XML 文档。|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **SecondOperand**  
 如果将“SecondOperandType”设置为“直接输入”，请提供 XML 代码，或单击省略号按钮 (…)，再使用“文档源编辑器”对话框提供 XML 代码。  
  
 如果将“SecondOperandType”设置为“文件连接”，请选择文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关的主题：**[文件连接管理器](connection-manager/file-connection-manager.md)，[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将“SecondOperandType”设置为“变量”，请选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题**:[Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)，[添加变量](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [“表达式”页](expressions/expressions-page.md)  
  
  
