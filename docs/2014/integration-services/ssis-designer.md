---
title: SSIS 设计器 | Microsoft Docs
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
- SQL Server Integration Services, SSIS Designer
- Business Intelligence Development Studio, Integration Services in
- tools [Integration Services], SSIS Designer
- SSIS, SSIS Designer
- SSIS Designer, about SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: 006d68ea-1b5c-4c1e-8079-3910288e012c
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ec6a23a1364e76f6f47014c3a4eeef52098e242d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014571"
---
# <a name="ssis-designer"></a>SSIS 设计器
  [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器是用于创建和维护 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的图形工具。 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器作为 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 项目的一部分，位于 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中。  
  
 可以使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器执行下列任务：  
  
-   在包中构造控制流。  
  
-   在包中构造数据流。  
  
-   将事件处理程序添加到包和包对象。  
  
-   查看包内容。  
  
-   在运行时查看包的执行进度。  
  
 下面的关系图显示 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器和 **“工具箱”** 窗口。  
  
 ![SSIS 设计器和工具箱的屏幕快照](media/denali-designerandtoolbox.gif "SSIS 设计器和工具箱的屏幕快照")  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 还有其他一些用于将功能添加到包的对话框和窗口，而 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 提供用于配置开发环境及对包进行操作的窗口和对话框。 有关详细信息，请参阅 [Integration Services 用户界面](integration-services-user-interface.md)。  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器不依赖于 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务（即管理和监视包的服务），而且在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中创建或修改包也不需要该服务处于运行状态。 但是，如果在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器打开的情况下停止该服务，则您无法再打开 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器提供的对话框，并且可能收到“RPC 服务器不可用”的错误消息。 若要重置 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器并继续对包进行操作，就必须关闭设计器，退出 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，然后重新打开 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目和包。  
  
## <a name="undo-and-redo"></a>撤消和重做  
 您可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中撤消或重做最多 20 个操作。 对于包，可以在“控制流”、“数据流”、“事件处理程序”和“参数”选项卡以及“变量”窗口中进行撤消/重做。 对于项目，可以在“项目参数”窗口中进行撤消/重做。  
  
 不能撤消/重做对新的“SSIS 工具箱”所做的更改。  
  
 使用组件编辑器更改组件时，可以将更改作为一个组来撤消和重做，而不是撤消和重做单个更改。 更改组在撤消和重做下拉列表中显示为单个操作。  
  
 若要撤消操作，请单击撤消工具栏按钮、“编辑/撤消”菜单项，或按 Ctrl+Z。 若要恢复操作，请单击恢复工具栏按钮、“编辑/恢复”菜单项或按 CTRL + Y。若要撤消和恢复多项操作，可以单击相应工具栏按钮旁边的箭头，在下拉列表中选中多项操作，然后在该列表中单击。  
  
## <a name="parts-of-the-ssis-designer"></a>SSIS 设计器的部件  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器有五个永久选项卡：其中四个选项卡分别用于生成包控制流、数据流、参数和事件处理程序，另外一个选项卡用于查看包的内容。 运行时将出现第六个选项卡，显示包在运行时的执行进度以及完成后的执行结果。  
  
 此外， [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器还包括连接管理器区域，用于添加和配置包连接到数据所使用的连接管理器。  
  
### <a name="control-flow-tab"></a>“控制流”选项卡  
 若要构造包中的控制流，即可在 **“控制流”** 选项卡的设计图面进行。先将所需项从 **“工具箱”** 逐个拖动到设计图面上，然后单击项的图标，将箭头从一项拖动到另一项，如此反复，将这些项连成一个控制流。  
  
 有关详细信息，请参阅 [Control Flow](control-flow/control-flow.md)。  
  
### <a name="data-flow-tab"></a>“数据流”选项卡  
 如果包中包含数据流任务，则可以将数据流添加到包。 在 **“数据流”** 选项卡设计图面上的包中构造数据流。先将所需项从 **“工具箱”** 逐个拖动到设计图面上，然后单击项的图标，将一项的箭头拖动到另一项，如此反复，将这些项连成一个数据流。  
  
 有关详细信息，请参阅 [Data Flow](data-flow/data-flow.md)。  
  
### <a name="parameters-tab"></a>“参数”选项卡  
 Integration Services (SSIS) 参数可用于在包执行时向包内的属性赋值。 您可以在项目级别创建项目参数，在包级别创建包参数。 项目参数可用于向项目中的一个或多个包提供项目接收的任何外部输入。 利用包参数，您不必编辑和重新部署包就可以修改包执行。 您可以利用此选项卡来管理包参数。  
  
 有关参数的详细信息，请参阅 [Integration Services (SSIS) 参数](integration-services-ssis-package-and-project-parameters.md)。  
  
> [!IMPORTANT]  
>  参数仅可用于为项目部署模型开发的项目。 因此，仅对于属于配置为使用项目部署模型的项目一部分的包，您才会看到“参数”选项卡。  
  
### <a name="event-handlers-tab"></a>“事件处理程序”选项卡  
 在 **“事件处理程序”** 选项卡设计图面上构造包中的事件。在 **“事件处理程序”** 选项卡上选择要为之创建事件处理程序的包或包对象，再选择要与事件处理程序相关联的事件。 一个事件处理程序有一个控制流，如果需要，还可以有多个可选的数据流。  
  
 有关详细信息，请参阅 [Add an Event Handler to a Package](../../2014/integration-services/add-an-event-handler-to-a-package.md)。  
  
### <a name="package-explorer-tab"></a>“包资源管理器”选项卡  
 包可以很复杂，包括多项任务、连接管理器、变量和其他元素。 在包的资源管理器视图中，可以查看完整的包元素列表。  
  
 有关详细信息，请参阅[查看包对象](view-package-objects.md)。  
  
#### <a name="progressexecution-result-tab"></a>“进度/执行结果”选项卡  
 在包运行过程中， **“进度”** 选项卡显示包的执行进度。 在包运行完毕后， **“执行结果”** 选项卡上就一直显示执行结果。  
  
> [!NOTE]  
>  若要允许或禁止在 **“进度”** 选项卡上显示消息，请在 **SSIS** 菜单上切换 **“调试进度报告”** 选项。  
  
##### <a name="connection-managers-area"></a>连接管理器区域  
 **“连接管理器”** 区域用于添加和修改包使用的连接管理器。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包括连接到多种数据源（如文本文件、OLE DB 数据库和 .Net 提供程序）的连接管理器。  
  
 有关详细信息，请参阅 [Integration Services (SSIS) 连接](connection-manager/integration-services-ssis-connections.md)和[创建连接管理器](../../2014/integration-services/create-connection-managers.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [在 SQL Server Data Tools 中创建包](create-packages-in-sql-server-data-tools.md)  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 用户界面](integration-services-user-interface.md)  
  
  