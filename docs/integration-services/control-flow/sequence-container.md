---
title: "序列容器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.sequencecontainer.f1"
helpviewer_keywords: 
  - "序列容器"
  - "对控制流进行分组"
  - "容器 [Integration Services], 序列"
  - "子集控制流 [Integration Services]"
ms.assetid: 7731f91e-b8b3-4d96-a0d9-73f568547cb3
caps.latest.revision: 48
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 48
---
# 序列容器
  序列容器可定义作为包控制流子集的控制流。 序列容器将包分组到多个单独的控制流中，每个控制流包含一个或多个在整体包控制流中运行的任务和容器。  
  
 除包含其他容器外，序列容器还可以包含多个任务。 将任务和容器添加到序列容器的过程与将它们添加到包的过程相似，唯一不同是把任务和容器拖动到序列容器，而不是拖动到包容器。 如果序列容器包含多个任务或容器，可以使用优先约束连接它们，如同在包中的操作一样。 有关详细信息，请参阅 [Precedence Constraints](../../integration-services/control-flow/precedence-constraints.md)。  
  
 使用序列容器有许多好处：  
  
-   禁用任务组，以便将包调试主要放在包控制流的一个子集上执行。  
  
-   通过设置序列容器而不是各个任务的属性来管理一个位置中多个任务的属性。  
  
     例如，可以将序列容器的 **Disable** 属性设置为 **True** ，以禁用序列容器中的所有任务和容器。  
  
-   提供一组相关任务和容器所用变量的范围。  
  
-   对许多任务进行分组，以便您可以通过展开和折叠序列容器，更轻松地管理这些任务。  
  
     也可以创建任务组，这些任务组用 **“分组”** 框展开和折叠。 但是，“分组”框是设计时功能，没有属性或运行时行为。 有关详细信息，请参阅[对组件分组或取消分组](../../integration-services/group-or-ungroup-components.md)  
  
-   在序列容器上设置事务属性，以便为包控制流的子集定义事务。 采用这种方法，可以更详细地管理事务。  
  
     例如，如果序列容器包含两个相关任务（一个任务删除表中的数据，另一个将数据插入到表中），则可配置事务以确保插入操作失败时回滚删除操作。 有关详细信息，请参阅 [Integration Services 事务](../../integration-services/integration-services-transactions.md)。  
  
## 序列容器的配置  
 序列容器没有自定义用户界面，您只能通过 **中的** “属性” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 窗口对其进行配置，或以编程方式配置。  
  
 有关以编程方式设置这些属性的详细信息，请参阅开发人员指南中针对 **T:Microsoft.SqlServer.Dts.Runtime.Sequence** 类的文档。  
  
## 相关任务  
 有关如何在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中设置组件属性的信息，请参阅[设置任务或容器的属性](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)。  
  
## 另请参阅  
 [在控制流中添加或删除任务或容器](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [使用默认优先约束来连接任务和容器](../Topic/Connect%20Tasks%20and%20Containers%20by%20Using%20a%20Default%20Precedence%20Constraint.md)   
 [Integration Services 容器](../../integration-services/control-flow/integration-services-containers.md)  
  
  