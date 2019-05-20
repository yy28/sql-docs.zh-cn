---
title: 平面文件目标 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.flatfiledest.f1
- sql13.dts.designer.flatfiledestadapter.connection.f1
- sql13.dts.designer.flatfiledestadapter.mappings.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5c432741bd8ba3d369230ac72e26ee5516d21d97
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726812"
---
# <a name="flat-file-destination"></a>平面文件目标

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  平面文件目标将数据写入文本文件。 文本文件可以为带分隔符格式、固定宽度格式、固定宽度并使用行分隔符格式或右边未对齐格式。  
  
 可以按照下列方式配置平面文件目标：  
  
-   提供在写入任何数据之前插入到文件的文本块。 该文本可以提供列标题之类信息。  
  
-   指定是否覆盖同名目标文件中的数据。  
  
 此目标用平面文件连接管理器访问文本文件。 通过设置平面文件目标所用平面文件连接管理器的属性，可以指定平面文件目标如何格式化和写入文本文件。 配置平面文件连接管理器时，请指定有关文件以及文件中每一列的信息。 例如，指定在文件中分隔列和行的字符，而且指定每列的数据类型和长度。 有关详细信息，请参阅 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)。  
  
 平面文件目标包括 Header 自定义属性。 加载包时，可以通过属性表达式更新此属性。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../integration-services/expressions/integration-services-ssis-expressions.md)、[在包中使用属性表达式](../../integration-services/expressions/use-property-expressions-in-packages.md)和[平面文件自定义属性](../../integration-services/data-flow/flat-file-custom-properties.md)。  
  
 此目标具有一个输出。 它不支持错误输出。  
  
## <a name="configuration-of-the-flat-file-destination"></a>配置平面文件目标  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [平面文件自定义属性](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何设置数据流组件属性的信息，请参阅 [设置数据流组件属性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="flat-file-destination-editor-connection-manager-page"></a>平面文件目标编辑器（“连接管理器”页）
  可以使用 **“平面文件目标编辑器”** 对话框的 **“连接管理器”** 页为目标选择平面文件连接，以及指定是覆盖现有目标文件还是追加到现有目标文件。 平面文件目标可以将数据写入文本文件。 该文本文件可以采用带分隔符、固定宽度、带有行分隔符的固定宽度或右边未对齐的格式。  
  
### <a name="options"></a>选项  
 **平面文件连接管理器**  
 使用列表框选择现有的连接管理器，或单击“新建”创建新的连接管理器。  
  
 **新建**  
 使用“平面文件格式”和“平面文件连接管理器编辑器”对话框创建新的连接。  
  
 **“平面文件格式”** 对话框中除了提供带分隔符、固定宽度和右边未对齐这三种标准的平面文件格式外，还提供了第四个选项： **“固定宽度并使用行分隔符”**。 此选项表示右边未对齐格式的一种特殊情况，在这种格式下， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将添加一个虚列作为最后一个数据列。 此虚列可确保最后一列具有固定宽度。  
  
 **“固定宽度并使用行分隔符”** 选项在 **“平面文件连接管理器编辑器”** 中不可用。 如果需要，可以在该编辑器中模拟此选项。 若要模拟此选项，请在 **“平面文件连接管理器编辑器”** 的 **“常规”** 页上，为 **“格式”** 选择 **“右边未对齐”**。 然后在该编辑器的 **“高级”** 页上，添加一个新的虚列作为最后一个数据列。  
  
 **覆盖文件中的数据**  
 指示是覆盖现有文件还是向现有文件中追加数据。  
  
 **标题**  
 键入在向文件中写入任何数据之前插入到该文件中的文本块。 使用此选项可以包括其他信息，如列标题。  
  
 **预览**  
 通过使用“数据视图”对话框预览结果。 预览最多可以显示 200 行。  
  
## <a name="flat-file-destination-editor-mappings-page"></a>平面文件目标编辑器（“映射”页）
  可以使用 **“平面文件目标编辑器”** 对话框的 **“映射”** 页，将输入列映射到目标列。  
  
### <a name="options"></a>选项  
 **可用输入列**  
 查看可用输入列的列表。 使用拖放操作将可用输入列映射到目标列。  
  
 **可用目标列**  
 查看可用目标列的列表。 使用拖放操作将可用目标列映射到输入列。  
  
 **输入列**  
 查看本主题中以前选择的输入列。 可以通过使用 **“可用输入列”** 列表来更改映射。 选择“\<ignore>”可以将该列排除在输出之外。  
  
 **目标列**  
 查看每个可用的目标列，包括已映射或未映射的目标列。  
  
## <a name="see-also"></a>另请参阅  
 [平面文件源](../../integration-services/data-flow/flat-file-source.md)   
 [数据流](../../integration-services/data-flow/data-flow.md)  
  
  
