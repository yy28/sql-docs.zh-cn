---
title: 平面文件源 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.flatfilesource.f1
- sql13.dts.designer.flatfilesourceadapter.connection.f1
- sql13.dts.designer.flatfilesourceadapter.columns.f1
- sql13.dts.designer.flatfilesourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], Flat File
- text file reading [Integration Services]
- flat files
- Flat File source
ms.assetid: 4a64f7f3-f25d-4db0-93b3-a29496030e58
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 04ad1cea264b46a097d78c475c346b0759b52f78
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35330661"
---
# <a name="flat-file-source"></a>平面文件源
  平面文件源从文本文件中读取数据。 文本文件可以为带分隔符格式、固定宽度格式或混合格式。  
  
-   带分隔符格式使用列和行分隔符定义列和行。  
  
-   固定宽度格式使用宽度定义列和行。 此格式还包含一个用于将字段填充到其最大宽度的字符。  
  
-   右边未对齐格式使用宽度定义除最后一列的所有列，最后一列由行分隔符分隔。  
  
 可以按照下列方式配置平面文件源：  
  
-   将一个列添加到转换输出（此转换输出包含平面文件源从中提取数据的文本文件的名称）中。  
  
-   指定平面文件源是否将列中长度为零的字符串解释为空值。  
  
    > [!NOTE]  
    >  若要将长度为零的字符串解释为空值，平面文件源使用的平面文件连接管理器必须配置为使用带分隔符格式。 如果连接管理器使用固定宽度或右边未对齐格式，那么由空格组成的数据便无法解释为空值。  
  
 平面文件源输出中的输出列包含 FastParse 属性。 FastParse 指示该列是使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的速度较快但不区分区域设置的较快分析例程，还是使用区分区域设置的标准分析例程。 有关详细信息，请参阅 [Fast Parse](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) 和 [Standard Parse](http://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)。  
  
 输出列还包含 UseBinaryFormat 属性。 使用该属性可在文件中实现对二进制数据（如带有组合型十进制格式的数据）的支持。 默认情况下 UseBinaryFormat 设置为 **false**。 如果要使用二进制格式，请将 UseBinaryFormat 设置为 **true** ，并将输出列的数据类型设置为 **DT_BYTES**。 执行上述操作时，平面文件源将跳过数据转换并将数据原样传递到输出列。 然后，可以使用“派生列”或“数据转换”等转换将 **DT_BYTES** 数据转换为不同的数据类型，或者在脚本转换中编写自定义脚本来解释数据。 也可以编写自定义数据流组件来解释数据。 有关可将 **DT_BYTES** 转换为哪些数据类型的详细信息，请参阅[转换（SSIS 表达式）](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 此源使用平面文件连接管理器访问文本文件。 通过设置平面文件连接管理器的属性，可以提供关于文件和文件中每列的信息，并可以指定平面文件源应如何处理文本文件中的数据。 例如，可以指定文件中分隔列和行的字符，以及每列的数据类型和长度。 有关详细信息，请参阅 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)。  
  
 此源具有一个输出和一个错误输出。  
  
## <a name="configuration-of-the-flat-file-source"></a>平面文件源的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [平面文件自定义属性](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何设置数据流组件属性的详细信息，请参阅 [设置数据流组件属性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="flat-file-source-editor-connection-manager-page"></a>平面文件源编辑器（“连接管理器”页）
  可以使用 **“平面文件源编辑器”** 对话框的 **“连接管理器”** 页，选择平面文件源将使用的连接管理器。 平面文件源从文本文件中读取数据，文本文件可以采用分隔符分隔、固定宽度或混合格式。  
  
 平面文件源可以使用下列类型的连接管理器之一：  
  
-   如果源是单个平面文件，则使用平面文件连接管理器。 有关详细信息，请参阅 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)。  
  
-   如果源是多平面文件并且数据流任务在循环容器（例如 For 循环容器）内，则使用多平面文件连接管理器。 在容器的每个循环中，平面文件源从多平面文件连接管理器提供的下一个文件名加载数据。 有关详细信息，请参阅 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)。  
  
### <a name="options"></a>“常规”  
 **Flat file connection manager**  
 从列表中选择现有的连接管理器，或单击“新建”创建新的连接管理器。  
  
 **新建**  
 通过使用“平面文件连接管理器编辑器”对话框创建新的连接管理器。  
  
 **在数据流中保留源中的空值**  
 指定提取数据时是否保留空值。 此属性的默认值为 **false**。 当此值为 F**alse**时，平面文件源使用每列的相应默认值替换源数据中的空值，例如，对于字符串列使用空字符串，对于数值列使用零。  
  
 **预览**  
 通过使用“数据视图”对话框预览结果。 预览最多可以显示 200 行。  
  
## <a name="flat-file-source-editor-columns-page"></a>平面文件源编辑器（“列”页）
  可以使用“平面文件源编辑器”对话框的“列”节点，将输出列映射到每个外部（源）列。  
  
> [!NOTE]  
>  平面文件源的 **FileNameColumnName** 属性及其输出列的 **FastParse** 属性未在 **“平面文件源编辑器”** 中提供，但可以使用 **“高级编辑器”** 进行设置。 有关这些属性的详细信息，请参阅 [Flat File Custom Properties](../../integration-services/data-flow/flat-file-custom-properties.md)的“平面文件源”部分。  
  
### <a name="options"></a>“常规”  
 **可用外部列**  
 查看数据源中可用外部列的列表。 无法使用此表添加或删除列。  
  
 **“外部列”**  
 按任务读取外部（源）列的顺序查看这些列。 首先清除表中所选的列，然后以不同的顺序从列表中选择外部列，即可更改顺序。  
  
 **输出列**  
 为每个输出列提供唯一的名称。 默认值为所选外部（源）列的名称；不过，您也可以任选一个唯一的描述性名称。 所提供的名称将在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中显示。  
  
## <a name="flat-file-source-editor-error-output-page"></a>平面文件源编辑器（“错误输出”页）
  可以使用“平面文件源编辑器”对话框的“错误输出”页选择错误处理选项，以及设置错误输出列的属性。  
  
### <a name="options"></a>“常规”  
 **输入/输出**  
 查看数据源的名称。  
  
 **列**  
 查看在“平面文件源编辑器”对话框中“连接管理器”页上选择的外部（源）列。  
  
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
 [平面文件目标](../../integration-services/data-flow/flat-file-destination.md)   
 [数据流](../../integration-services/data-flow/data-flow.md)  
  
  
