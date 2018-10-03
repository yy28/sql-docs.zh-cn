---
title: 平面文件源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfilesource.f1
helpviewer_keywords:
- sources [Integration Services], Flat File
- text file reading [Integration Services]
- flat files
- Flat File source
ms.assetid: 4a64f7f3-f25d-4db0-93b3-a29496030e58
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a8a06ae3b308c90b2dc789c97f5f262530826229
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48125407"
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
  
 平面文件源输出中的输出列包含 FastParse 属性。 FastParse 指示该列是使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的速度较快但不区分区域设置的较快分析例程，还是使用区分区域设置的标准分析例程。 有关详细信息，请参阅 [Fast Parse](../fast-parse.md) 和 [Standard Parse](../standard-parse.md)。  
  
 输出列还包含 UseBinaryFormat 属性。 使用该属性可在文件中实现对二进制数据（如带有组合型十进制格式的数据）的支持。 默认情况下 UseBinaryFormat 设置为`false`。 如果你想要使用二进制格式，请将 UseBinaryFormat 设置为`true`的数据类型的输出列和`DT_BYTES`。 执行上述操作时，平面文件源将跳过数据转换并将数据原样传递到输出列。 然后，可以使用“派生列”或“数据转换”等转换将 `DT_BYTES` 数据转换为不同的数据类型，或者在脚本转换中编写自定义脚本来解释数据。 也可以编写自定义数据流组件来解释数据。 有关可以转换为哪些数据类型的详细信息`DT_BYTES`以，请参阅[转换&#40;SSIS 表达式&#41;](../expressions/cast-ssis-expression.md)。  
  
 此源使用平面文件连接管理器访问文本文件。 通过设置平面文件连接管理器的属性，可以提供关于文件和文件中每列的信息，并可以指定平面文件源应如何处理文本文件中的数据。 例如，可以指定文件中分隔列和行的字符，以及每列的数据类型和长度。 有关详细信息，请参阅 [Flat File Connection Manager](../connection-manager/file-connection-manager.md)。  
  
 此源具有一个输出和一个错误输出。  
  
## <a name="configuration-of-the-flat-file-source"></a>平面文件源的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可在 **“平面文件源编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [平面文件源编辑器&#40;连接管理器页&#41;](../flat-file-source-editor-connection-manager-page.md)  
  
-   [平面文件源编辑器&#40;列页&#41;](../flat-file-source-editor-columns-page.md)  
  
-   [平面文件源编辑器&#40;错误输出页&#41;](../flat-file-source-editor-error-output-page.md)  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](../common-properties.md)  
  
-   [平面文件自定义属性](flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何设置数据流组件属性的详细信息，请参阅 [设置数据流组件属性](set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>请参阅  
 [平面文件目标](flat-file-destination.md)   
 [数据流](data-flow.md)  
  
  
