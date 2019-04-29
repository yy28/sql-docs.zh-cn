---
title: 通过在任务或容器上设置断点调试包 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], breakpoints
- breakpoints [Integration Services]
- tasks [Integration Services], breakpoints
ms.assetid: e7fa106a-2221-403a-bb74-efc9f12bb450
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3c78fb92078c604d881f18ea3472e23619771b49
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62898885"
---
# <a name="debug-a-package-by-setting-breakpoints-on-a-task-or-a-container"></a>通过在任务或容器上设置断点调试包
  本过程介绍如何在包、任务、For 循环容器、Foreach 循环容器或序列容器中设置断点。  
  
### <a name="to-set-breakpoints-in-a-package-a-task-or-a-container"></a>在包、任务或容器中设置断点  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  双击包含要在其中设置断点的包。  
  
3.  在 SSIS 设计器中，执行下列操作：  
  
    -   若要在包对象中设置断点，请单击“控制流”选项卡，将光标置于设计图面背景的任意位置，右键单击，再单击“编辑断点”。  
  
    -   若要在包控制流中设置断点，请单击“控制流”选项卡，右键单击任务、For 循环容器、Foreach 循环容器或序列容器，再单击“编辑断点”。  
  
    -   若要在事件处理程序中设置断点，请单击“事件处理程序”选项卡，右键单击任务、For 循环容器、Foreach 循环容器或序列容器，再单击“编辑断点”。  
  
4.  在“设置断点 \<容器名称>”对话框中，选择要启用的断点。  
  
5.  还可以修改每个断点的命中计数类型和命中计数数量。  
  
6.  若要保存包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>请参阅  
 [包开发的故障排除工具](troubleshooting/troubleshooting-tools-for-package-development.md)   
 [通过在脚本任务和脚本组件中设置断点来调试脚本](data-flow/transformations/script-component.md)   
 [脚本任务的编码和调试](control-flow/script-task.md)   
 [脚本组件的编码和调试](extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
