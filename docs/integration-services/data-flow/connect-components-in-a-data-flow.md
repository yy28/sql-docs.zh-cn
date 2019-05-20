---
title: 连接数据流中的组件 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 70616a58-8921-4218-85bf-f3e90c5a9dbf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8d353876938b3e64317f461240b2333e71217449
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727122"
---
# <a name="connect-components-in-a-data-flow"></a>连接数据流中的组件

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  本过程介绍如何将数据流中的组件输出连接到同一数据流中的其他组件。  
在 **设计器中** “数据流” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 选项卡的设计图面上构造包中的数据流。 如果数据流包含两个数据流组件，则可以将源或转换的输出连接到转换或目标的输入，以连接这两个组件。 两个数据流组件之间的连接器称为路径。  
  
 下面的关系图显示一个简单的数据流，它具有一个源组件、两个转换、一个目标组件以及连接它们的路径。  
  
 ![Data flow](../../integration-services/data-flow/media/mw-dts-08.gif "Data flow")  
  
 连接两个组件后，即可在 **“数据流路径编辑器”** 中查看通过路径移动的数据的元数据以及路径的属性。 有关详细信息，请参阅 [Integration Services Paths](../../integration-services/data-flow/integration-services-paths.md)。  
  
 还可以将数据查看器添加到路径。 数据查看器使您可以在包运行时查看在数据流组件间移动的数据。  
  
### <a name="connect-components-in-a-data-flow"></a>连接数据流中的组件  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击“控制流”选项卡，然后双击包含要连接的组件所在数据流的数据流任务。  
  
4.  在 **“数据流”** 选项卡的设计图面上，选择要连接的转换或源。  
  
5.  将转换或源的绿色输出箭头拖动到转换或目标。 某些数据流组件有错误输出，这些输出可通过同样方式连接。  
  
    > [!NOTE]  
    >  某些数据流组件可能有多个输出，您可以将每一个输出连接到不同的转换或目标。  
  
6.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>另请参阅  
 [在数据流中添加或删除组件](../../integration-services/data-flow/add-or-delete-a-component-in-a-data-flow.md)   
 [调试数据流](../../integration-services/troubleshooting/debugging-data-flow.md)[Data Flow](../../integration-services/data-flow/data-flow.md)  
  
  
