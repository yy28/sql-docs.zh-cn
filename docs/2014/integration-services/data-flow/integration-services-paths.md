---
title: Integration Services 路径 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- paths [Integration Services], about paths
- data flow [Integration Services], paths
- paths [Integration Services]
- destinations [Integration Services], paths
- sources [Integration Services], paths
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 33ce96096c0675b16d58532a351c20d897afb46a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025970"
---
# <a name="integration-services-paths"></a>Integration Services 路径
  路径将一个数据流组件的输出连接到另一个组件的输入，以此连接数据流中的两个组件。 路径具有源和目标。 例如，如果路径连接一个 OLE DB 源和一个排序转换，那么 OLE DB 源就是路径的源，而排序转换就是路径的目标。 源是路径开始处的组件，而目标是路径结束处的组件。  
  
 如果在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中运行包，您可以将数据查看器附加到一个路径，以此来查看数据流中的数据。 数据查看器可配置为在网格中显示数据。 数据查看器是个很有用的调试工具。 有关详细信息，请参阅 [Debugging Data Flow](../troubleshooting/debugging-data-flow.md)。  
  
## <a name="configuration-of-the-path"></a>路径的配置  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器提供 **“数据流路径编辑器”** 对话框，用于设置路径属性、查看通过该路径的数据列的元数据以及配置数据查看器。  
  
 可配置的路径属性有路径的名称、说明和批注。 还可以用编程的方式配置路径。 有关详细信息，请参阅 [以编程方式连接数据流组件](../building-packages-programmatically/connecting-data-flow-components-programmatically.md)。  
  
 路径批注显示路径源的名称或 **设计器中** “数据流” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 选项卡的设计图面上的路径名称。 路径批注与可以添加到数据流、控制流和事件处理程序的批注类似， 唯一区别是路径批注附加到路径，而其他批注则显示在 **设计器的**“数据流” **、**“控制流” **和**“事件处理程序” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 选项卡上。  
  
 元数据显示前一组件的输出中每一列的名称、数据类型、精度、小数位数、长度、代码页和源组件。 源组件是创建此列的数据流组件。 这可能是数据流中的第一个组件，也可能不是。 例如，Union All 和排序转换创建自己的列，并且是其输出列的源。 反之，复制列转换则可以不加更改地传递列，或者通过复制输入列来创建新列。 复制列转换仅是新列的源组件。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可在 **“数据流路径编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [数据流路径编辑器&#40;常规页&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [数据流路径编辑器&#40;元数据页&#41;](../data-flow-path-editor-metadata-page.md)  
  
-   [数据流路径编辑器&#40;数据查看器页&#41;](../data-flow-path-editor-data-viewers-page.md)  
  
 有关可以编程方式设置的属性的详细信息，请参阅 [Path Properties](../path-properties.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [在数据流路径编辑器中查看路径元数据](../view-path-metadata-in-the-data-flow-path-editor.md)  
  
-   [连接数据流中的组件](connect-components-in-a-data-flow.md)  
  
## <a name="see-also"></a>请参阅  
 [数据流](data-flow.md)  
  
  