---
title: "\"事件处理程序\" 选项卡 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.eventhandlerwindow.f1
ms.assetid: 94fc8916-8032-490c-b9d5-ded8b6217e49
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8777e6c0515a602198e3ed393714544d774f9958
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437414"
---
# <a name="event-handlers-tab"></a>“事件处理程序”选项卡
  可以使用 **设计器的** “事件处理程序” [!INCLUDE[ssIS](../includes/ssis-md.md)] 选项卡在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包中生成控制流。 事件处理程序可因响应由包、包中的任务或容器所引发的事件而运行。  
  
## <a name="options"></a>选项  
 **可执行文件**  
 选择要为其生成事件处理程序的可执行文件。 可执行文件可以是包、包中的任务或容器。  
  
 **事件处理程序**  
 选择事件处理程序的类型。 通过从 **“工具箱”** 中拖动相应项即可创建事件处理程序。  
  
 **删除**  
 选择一个事件处理程序，再通过单击“删除”**** 将其从包中删除。  
  
 **单击此处为 \<event handler name> 可执行文件创建\<executable name>**  
 单击此项可创建事件处理程序。  
  
 通过将代表 [!INCLUDE[ssIS](../includes/ssis-md.md)] 任务和容器的图形对象从 **“工具箱”** 拖至 **“事件处理程序”** 选项卡的设计图面，再通过使用优先约束定义其运行顺序来连接这些对象，即可创建控制流。  
  
 此外，通过右键单击设计图面，然后在菜单上单击“添加批注”****，以添加批注。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS&#41; 事件处理程序](integration-services-ssis-event-handlers.md)   
 [控制流](control-flow/control-flow.md)   
 [SSIS 设计器](ssis-designer.md)   
 [Integration Services (SSIS) 事件处理程序](integration-services-ssis-event-handlers.md)  
  
  
