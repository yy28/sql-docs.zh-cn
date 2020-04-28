---
title: 用路径连接组件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data flow [Integration Services], connections
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 05633e4c-1370-4b05-802b-f36b07dd71c8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e6cc08adc2682b65b1e2de9a2c3fd1d483a33c92
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176480"
---
# <a name="connect-components-with-paths"></a>使用路径连接组件
  在 **设计器中** “数据流” [!INCLUDE[ssIS](../includes/ssis-md.md)] 选项卡的设计图面上构造包中的数据流。 如果数据流包含两个数据流组件，则可以将源或转换的输出连接到转换或目标的输入，以连接这两个组件。 两个数据流组件之间的连接器称为路径。

 下面的关系图显示一个简单的数据流，它具有一个源组件、两个转换、一个目标组件以及连接它们的路径。

 ![数据流](media/mw-dts-08.gif "数据流")

 连接两个组件后，即可在 **“数据流路径编辑器”** 中查看通过路径移动的数据的元数据以及路径的属性。 有关详细信息，请参阅 [Integration Services Paths](data-flow/integration-services-paths.md)。

 还可以将数据查看器添加到路径。 数据查看器使您可以在包运行时查看在数据流组件间移动的数据。

### <a name="to-connect-components-in-a-data-flow"></a>连接数据流中的组件

-   [连接数据流中的组件](data-flow/connect-components-in-a-data-flow.md)

### <a name="to-set-path-properties"></a>设置路径属性

-   [使用数据流路径编辑器设置路径属性](../../2014/integration-services/set-the-properties-of-a-path-by-using-the-data-flow-path-editor.md)

### <a name="to-view-path-metadata"></a>查看路径元数据

-   [在数据流路径编辑器中查看路径元数据](../../2014/integration-services/view-path-metadata-in-the-data-flow-path-editor.md)

### <a name="to-view-path-metadata"></a>查看路径元数据

-   [将数据查看器添加到数据流](../../2014/integration-services/add-a-data-viewer-to-a-data-flow.md)

## <a name="see-also"></a>另请参阅
 数据流[任务](control-flow/data-flow-task.md)数据流转换数据[时转换数据](data-flow/data-flow.md)中[的](data-flow/transformations/transform-data-with-transformations.md)[错误处理](data-flow/error-handling-in-data.md)


