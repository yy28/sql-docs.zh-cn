---
title: "通过在任务或容器上设置断点调试包 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "容器 [Integration Services], 断点"
  - "断点 [Integration Services]"
  - "任务 [Integration Services], 断点"
ms.assetid: e7fa106a-2221-403a-bb74-efc9f12bb450
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# 通过在任务或容器上设置断点调试包
  本过程介绍如何在包、任务、For 循环容器、Foreach 循环容器或序列容器中设置断点。  
  
### 在包、任务或容器中设置断点  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  双击包含要在其中设置断点的包。  
  
3.  在 SSIS 设计器中，执行下列操作：  
  
    -   若要在包对象中设置断点，请单击“控制流”选项卡，将光标置于设计图面背景的任意位置，右键单击，再单击“编辑断点”。  
  
    -   若要在包控制流中设置断点，请单击“控制流”选项卡，右键单击任务、For 循环容器、Foreach 循环容器或序列容器，再单击“编辑断点”。  
  
    -   若要在事件处理程序中设置断点，请单击“事件处理程序”选项卡，右键单击任务、For 循环容器、Foreach 循环容器或序列容器，再单击“编辑断点”。  
  
4.  在“设置断点 \<容器名称>”对话框框中，选择要启用的断点。  
  
5.  还可以修改每个断点的命中计数类型和命中计数数量。  
  
6.  若要保存包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## 另请参阅  
 [包开发的故障排除工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)   
 [通过在脚本任务和脚本组件中设置断点来调试脚本](../../integration-services/extending-packages-scripting/debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component.md)   
 [脚本任务的编码和调试](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)   
 [脚本组件的编码和调试](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  