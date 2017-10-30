---
title: "复制列转换 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.copycolumntrans.f1
- sql13.dts.designer.copymaptransformation.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: d05d290cd9468eb7fd0b208e00a88db76cfae61a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/19/2017

---
# <a name="copy-column-transformation"></a>复制列转换
  复制列转换通过复制输入列并将新列添加到转换输出来创建新列。 以后在数据流中，可将不同的转换应用到列副本。 例如，您可以使用复制列转换来创建列的副本，然后使用字符映射表转换将复制的数据转换为大写字符，或使用聚合转换将聚合应用到此新列。  
  
## <a name="configuration-of-the-copy-column-transformation"></a>复制列转换的配置  
 可以通过指定要复制的输入列来配置复制列转换。 可以在一个操作中创建一列的多个副本，或创建多个列的副本。  
  
 此转换有一个输入和一个输出。 它不支持错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [转换自定义属性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="copy-column-transformation-editor"></a>复制列转换编辑器
  可以使用 **“复制列转换编辑器”** 对话框选择要复制的列，以及为新的输出列指定名称。  
  
> [!NOTE]  
>  如果只是将所有源数据复制到目标，可能无需使用复制列转换。 某些情况下，如果不需要进行任何数据转换，可以直接将源连接到目标。 在这些情况下，使用 SQL Server 导入和导出向导创建包通常更可取。 以后，您可以根据需要增强并重新配置包。 有关更多信息，请参见 [SQL Server Import and Export Wizard](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)。  
  
### <a name="options"></a>选项  
 **可用输入列**  
 使用复选框选择要复制的列。 选择后，会将输入列添加到下表中。  
  
 **输入列**  
 从可用的输入列列表中选择要复制的列。 通过选中 **“可用输入列”** 表中的复选框来选择列。  
  
 **输出别名**  
 为每个新的输出列键入一个别名。 默认值为输入列名称后面跟着 **“的副本”**；不过，您也可以任选一个唯一的描述性名称。  
  
## <a name="see-also"></a>另请参阅  
 [数据流](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 转换](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  

