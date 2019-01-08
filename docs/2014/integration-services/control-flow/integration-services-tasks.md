---
title: Integration Services 任务 | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [Integration Services], tasks
- files [Integration Services], task options
- workflow tasks [Integration Services]
- Integration Services, tasks
- adding package tasks
- tasks [Integration Services], listed
- SSIS tasks
- SSIS, tasks
- control flow [Integration Services], tasks
- tasks [Integration Services]
- grouping tasks
- tasks [Integration Services], about tasks
- SQL Server Integration Services tasks
- data preparation tasks [Integration Services]
- directory operations [Integration Services]
ms.assetid: 75c8901d-6966-4af3-abe5-10af6dd9313b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d840663c675452b137a57fedc56f623b430af6e4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52765639"
---
# <a name="integration-services-tasks"></a>Integration Services 任务
  任务是一些控制流元素，它定义包控制流中执行的工作单元。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包由一个或多个任务组成。 如果包中包含多个任务，则它们将按照优先约束在控制流中进行连接和排序。  
  
 您还可使用支持 COM 的编程语言（如 Visual Basic）或 .NET 编程语言（如 C#）编写自定义任务。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中用于处理包的图形工具，可提供用于创建包控制流的设计界面，以及用于配置任务的自定义编辑器。 您还可以对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 对象模型进行编程，以便通过编程方式创建包。  
  
## <a name="types-of-tasks"></a>任务的类型  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中包括下列类型的任务。  
  
 数据流任务  
 数据流任务用于运行数据流以提取数据、应用列级转换和加载数据。  
  
 数据准备任务  
 这些任务执行以下过程：复制文件和目录；下载文件和数据；运行 Web 方法；对 XML 文档应用操作以及对数据进行事件探查以便清除。  
  
 工作流任务  
 工作流任务与其他进程通信以运行包、程序或批处理文件，在包之间发送和接收消息，发送电子邮件，读取 Windows Management Instrumentation (WMI) 数据和监视 WMI 事件。  
  
 SQL Server 任务  
 SQL Server 任务用于访问、复制、插入、删除和修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象和数据。  
  
 脚本任务  
 脚本任务通过使用脚本来扩展包功能。  
  
 Analysis Services 任务  
 该任务用于创建、修改、删除和处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象。  
  
 维护任务  
 维护任务用于执行管理功能，如备份和收缩 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库、重新生成和重新组织索引以及运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业。  
  
 自定义任务  
 此外，您还可以使用支持 COM 的编程语言（如 Visual Basic）或 .NET 编程语言（如 C#）编写自定义任务。 如果希望在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中访问自定义任务，那么你可以为该任务创建和注册一个用户接口。 有关详细信息，请参阅 [开发自定义任务](../extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="configuration-of-tasks"></a>任务的配置  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包可以只包含单个任务，如在包运行时删除数据库表中记录的执行 SQL 任务。 但是，包通常包含多个任务，而且每个任务都被设置为在包控制流上下文中运行。 事件处理程序是为响应运行时事件而运行的工作流，该程序中也可包含任务。  
  
 有关使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器向包添加任务的详细信息，请参阅 [在控制流中添加或删除任务或容器](add-or-delete-a-task-or-a-container-in-a-control-flow.md)。  
  
 有关如何以编程方式向包中添加任务的详细信息，请参阅 [以编程方式添加任务](../building-packages-programmatically/adding-tasks-programmatically.md)。  
  
 对于每个任务，可以使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器为每个任务提供的自定义对话框单独配置，也可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中包含的“属性”窗口进行配置。 一个包中可以包含多个相同类型的任务（如六个执行 SQL 任务），对每个任务可进行不同的配置。 有关详细信息，请参阅 [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)。  
  
## <a name="tasks-connections-and-groups"></a>任务连接和组  
 如果连接和分组任务中包含多个任务，则它们将被按照优先约束在控制流中进行连接和排序。 有关详细信息，请参阅 [优先约束](precedence-constraints.md)。  
  
 任务可被分组到一起作为一个工作单元执行，也可在循环中重复执行。 有关详细信息，请参阅 [Foreach Loop Container](foreach-loop-container.md)、 [For Loop Container](for-loop-container.md)和 [Sequence Container](sequence-container.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
 [在控制流中添加或删除任务或容器](add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
  
