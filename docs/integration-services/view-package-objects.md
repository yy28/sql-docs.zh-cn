---
title: "查看包对象 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services 包, 属性"
  - "属性 [Integration Services]"
  - "“包资源管理器”窗口 [Integration Services]"
  - "包 [Integration Services], 属性"
  - "资源管理器视图 [Integration Services]"
  - "SSIS 包, 属性"
  - "查看包对象"
  - "SQL Server Integration Services 包, 属性"
ms.assetid: a85c0245-0a68-4eb0-83b1-9b11df80bd10
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# 查看包对象
  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中， **“包资源管理器”** 选项卡提供包的资源管理器视图。 该视图反映了 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 体系结构的容器层次结构。 包容器位于层次结构的顶层，您可以展开包来查看连接、可执行文件、事件处理程序、日志提供程序、优先约束和包中的变量。  
  
 可执行文件（包中的容器和任务）可以包含事件处理程序、优先约束和变量。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 支持嵌套的容器层次结构，而 For 循环容器、Foreach 循环容器以及序列容器可包含其他可执行文件。  
  
 如果包包含数据流， **包资源管理器** 将列出数据流任务，并包含列有数据流组件的 **“组件”** 文件夹。  
  
 可以从 **“包资源管理器”** 选项卡中删除包中的对象，并访问 **“属性”** 窗口来查看对象属性。  
  
 下面的关系图显示一个简单包的树视图。  
  
 ![“包资源管理器”选项卡的屏幕快照](../integration-services/media/packageexplorer.gif "“包资源管理器”选项卡的屏幕快照")  
  
### 查看包内容  
  
-   [在包资源管理器中查看包对象](../Topic/View%20Package%20Objects%20in%20Package%20Explorer.md)  
  
## 另请参阅  
 [Integration Services 任务](../integration-services/control-flow/integration-services-tasks.md)   
 [Integration Services 容器](../integration-services/control-flow/integration-services-containers.md)   
 [优先约束](../integration-services/control-flow/precedence-constraints.md)   
 [Integration Services (SSIS) 变量](../integration-services/integration-services-ssis-variables.md)   
 [Integration Services (SSIS) 事件处理程序](../integration-services/integration-services-ssis-event-handlers.md)   
 [Integration Services (SSIS) 日志记录](../integration-services/performance/integration-services-ssis-logging.md)  
  
  