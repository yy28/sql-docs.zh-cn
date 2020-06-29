---
title: 向包中添加事件处理程序 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- event handlers [Integration Services], creating
ms.assetid: 5e56885d-8658-480a-bed9-3f2f8003fd78
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 378b8c95f5b7f4ed1e247a89f3e3ad6111654303
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439704"
---
# <a name="add-an-event-handler-to-a-package"></a>在包中添加事件处理程序
  在运行时，容器和任务引发事件。 您可以创建自定义事件处理程序，这些程序在事件被引发时运行工作流，以对事件做出响应。 例如，您可创建一个事件处理程序，在任务失败时发送电子邮件。  
  
 事件处理程序与包类似。 事件处理程序可以像包一样为变量提供作用域，并且包含控制流和可选数据流。 您可以为包、Foreach 循环容器、For 循环容器和序列容器以及所有的任务生成事件处理程序。  
  
 您可以使用 **设计器中的** “事件处理程序” [!INCLUDE[ssIS](../includes/ssis-md.md)] 选项卡的设计图面来创建事件处理程序。  
  
 当 **“事件处理程序”** 选项卡活动时， **设计器中的工具箱的** “控制流项” **和** “维护计划中的任务” [!INCLUDE[ssIS](../includes/ssis-md.md)] 节点包含用于生成事件处理程序中控制流的任务和容器。 **“数据流源”**、 **“转换”** 和 **“数据流目标”** 节点包含用于生成事件处理程序中数据流的数据源、转换和目标。 有关详细信息，请参阅 [Control Flow](control-flow/control-flow.md) 和 [Data Flow](data-flow/data-flow.md)。  
  
 **“事件处理程序”** 选项卡也包含 **“连接管理器”** 区域，在这里可创建并修改事件处理程序用来连接到服务器和数据源的连接管理器。 有关详细信息，请参阅 [创建连接管理器](../../2014/integration-services/create-connection-managers.md)。  
  
### <a name="to-create-an-event-handler"></a>创建事件处理程序  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“事件处理程序”** 选项卡。  
  
     ![带有事件处理程序的设计图面的屏幕快照](media/eventhandlers.gif "带有事件处理程序的设计图面的屏幕快照")  
  
     在事件处理程序中创建控制流和数据流类似于在包中创建控制流和数据流。 有关详细信息，请参阅 [Control Flow](control-flow/control-flow.md) 和 [Data Flow](data-flow/data-flow.md)。  
  
4.  在 **“可执行文件”** 列表中，选择要为其创建事件处理程序的可执行文件。  
  
5.  在 **“事件处理程序”** 列表中，选择要生成的事件处理程序。  
  
6.  单击 **“事件处理程序”** 选项卡的设计图面上的链接。  
  
7.  将控制流项添加到事件处理程序，并且通过将优先约束从一个控制流项拖到另一控制流项，使用该约束来连接这些控制流项。 有关详细信息，请参阅 [Control Flow](control-flow/control-flow.md)。  
  
8.  还可以根据需要添加数据流任务，并且在 **“数据流”** 选项卡的设计图面上，为事件处理程序创建数据流。 有关详细信息，请参阅 [Data Flow](data-flow/data-flow.md)。  
  
9. 在 **“文件”** 菜单上，单击 **“保存选定项”** 以保存包。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Integration Services](../../2014/integration-services/sql-server-integration-services.md)   
 [Integration Services (SSIS) 日志记录](performance/integration-services-ssis-logging.md)  
  
  
