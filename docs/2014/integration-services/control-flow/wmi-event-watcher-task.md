---
title: WMI 事件观察器任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmieventwatchertask.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Event Watcher task [Integration Services]
ms.assetid: b5bb52e9-a77e-41e1-93f9-d4c3bc6b2c9a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4add98b6c085d52238a528c313008bc688ae6e54
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62829507"
---
# <a name="wmi-event-watcher-task"></a>WMI 事件观察器任务
  WMI 事件观察器任务以使用 Management Instrumentation 查询语言 (WQL) 事件查询指定所关注事件的方式来监视 Windows Management Instrumentation (WMI) 事件。 可以将 WMI 事件观察器任务用于下列目的：  
  
-   等待已将文件添加到文件夹的通知，然后开始处理文件。  
  
-   当服务器上的可用内存低于指定百分比时，运行删除文件的包。  
  
-   监视应用程序的安装，然后运行使用该应用程序的包。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含读取 WMI 信息的任务。  
  
 有关此任务的详细信息，请单击下列主题：  
  
-   [WMI 数据读取器任务](wmi-data-reader-task.md)  
  
## <a name="wql-queries"></a>WQL 查询  
 WQL 是 SQL 的方言，其扩展插件支持 WMI 事件通知和其他 WMI 特定功能。 有关 WQL 的详细信息，请参阅 [MSDN Library](https://go.microsoft.com/fwlink/?linkid=62553)中的 Windows Management Instrumentation 文档。  
  
> [!NOTE]  
>  WMI 类因 Windows 版本的不同而异。  
  
 以下查询监视 CPU 使用率超过 40% 的通知。  
  
```  
SELECT * from __InstanceModificationEvent WITHIN 2 WHERE TargetInstance ISA 'Win32_Processor' and TargetInstance.LoadPercentage > 40  
```  
  
 以下查询监视已将文件添加到文件夹的通知。  
  
```  
SELECT * FROM __InstanceCreationEvent WITHIN 10 WHERE TargetInstance ISA "CIM_DirectoryContainsFile" and TargetInstance.GroupComponent= "Win32_Directory.Name=\"c:\\\\WMIFileWatcher\""   
```  
  
## <a name="custom-logging-messages-available-on-the-wmi-event-watcher-task"></a>WMI 事件观察器任务可用的自定义日志记录消息  
 下表列出了 WMI 事件观察器任务的自定义日志项。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../performance/integration-services-ssis-logging.md)和[日志记录的自定义消息](../custom-messages-for-logging.md)。  
  
|日志项|说明|  
|---------------|-----------------|  
|`WMIEventWatcherEventOccurred`|指示发生了任务正在监视的事件。|  
|`WMIEventWatcherTimedout`|指示任务已超时。|  
|`WMIEventWatcherWatchingForWMIEvents`|指示任务已开始执行 WQL 查询。 日志项包括查询。|  
  
## <a name="configuration-of-the-wmi-event-watcher-task"></a>WMI 事件观察器任务的配置  
 可以通过以下方式配置 WMI 数据读取器任务：  
  
-   指定要使用的 WMI 连接管理器。  
  
-   指定 WQL 查询的源。 源可以在任务外部，比如变量或文件，否则可把查询存储在任务属性中。  
  
-   指定在 WMI 事件发生时任务所执行的操作。 可以记录事件通知和事件后的状态，也可以引发自定义 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 事件来提供与 WMI 事件、通知和事件后的状态相关的信息。  
  
-   定义任务对事件的响应方式。 可根据事件的不同将任务配置为成功或失败，或只是让任务重新监视事件。  
  
-   指定当 WMI 查询超时时任务所执行的操作。可以记录超时和超时后的状态，也可以引发自定义[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]事件，以指示 WMI 事件已超时并记录超时和超时状态。  
  
-   定义任务对超时的响应方式。可以将任务配置为成功或失败，或者任务可以立即监视事件。  
  
-   指定任务监视事件的次数。  
  
-   指定超时。  
  
 如果源是文件，则 WMI 事件观察器任务使用文件连接管理器连接到该文件。 有关详细信息，请参阅 [Flat File Connection Manager](../connection-manager/file-connection-manager.md)。  
  
 WMI 事件观察器任务使用 WMI 连接管理器连接到它从中读取 WMI 信息的服务器。 有关详细信息，请参阅 [WMI Connection Manager](../connection-manager/wmi-connection-manager.md)。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [WMI 事件观察器任务编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)  
  
-   [WMI 事件观察器任务编辑器（“WMI 选项”页）](../wmi-event-watcher-task-editor-wmi-options-page.md)  
  
-   [“表达式”页](../expressions/expressions-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-wmi-event-watcher-task"></a>WMI 事件观察器任务的编程配置  
 有关以编程方式设置这些属性的详细信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiEventWatcherTask.WmiEventWatcherTask>  
  
  
