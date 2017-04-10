---
title: "WMI 事件观察器任务编辑器（“WMI 选项”页） | Microsoft Docs"
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
  - "sql13.dts.designer.wmieventwatcher.wmiquery.f1"
helpviewer_keywords: 
  - "WMI 事件观察器任务编辑器"
ms.assetid: 525f3de7-a021-4e52-9939-3a83c88f131a
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# WMI 事件观察器任务编辑器（“WMI 选项”页）
  可以使用“WMI 事件观察器任务编辑器”对话框的“WMI 选项”页，指定 Windows Management Instrumentation 查询语言 (WQL) 查询的源以及 WMI 事件观察器任务响应 Microsoft Windows Instrumentation (WMI) 事件的方式。  
  
 若要了解此任务，请参阅 [WMI Event Watcher Task](../../integration-services/control-flow/wmi-event-watcher-task.md)。 有关 WMI 查询语言 (WQL) 的详细信息，请参阅 MSDN 库中的 Windows Management Instrumentation 主题 [Querying with WQL](http://go.microsoft.com/fwlink/?LinkId=79045)（利用 WQL 进行查询）。  
  
## 静态选项  
 **WMIConnectionName**  
 在列表中选择一个 WMI 连接管理器，或单击“\<新建 WMI 连接…>”新建一个连接管理器。  
  
 **相关主题：**[WMI 连接管理器](../../integration-services/connection-manager/wmi-connection-manager.md)和 [WMI 连接管理器编辑器](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 选择任务运行的 WQL 查询的源类型。 此属性具有下表所列的选项。  
  
|“值”|Description|  
|-----------|-----------------|  
|**直接输入**|为 WQL 查询设置源。 选择此值将显示动态选项 **WQLQuerySource**。|  
|**文件连接**|选择包含 WQL 查询的文件。 选择此值将显示动态选项 **WQLQuerySource**。|  
|**变量**|将源设置为定义 WQL 查询的变量。 选择此值将显示动态选项 **WQLQuerySource**。|  
  
 **ActionAtEvent**  
 指定 WMI 事件是记录事件并启动 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 操作，还是只记录事件。  
  
 **AfterEvent**  
 指定任务在收到 WMI 事件之后是成功还是失败，或者任务是否继续监视事件的再次发生。  
  
 **ActionAtTimeout**  
 指定任务是记录 WMI 查询超时并启动 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 事件作为响应，还是只记录超时。  
  
 **AfterTimeout**  
 指定任务对超时的响应是成功还是失败，或者任务是否继续监视超时的再次发生。  
  
 **NumberOfEvents**  
 指定要监视的事件数。  
  
 **超时**  
 指定等待事件发生的秒数。 值为 0 表示实际上无超时。  
  
## WQLQuerySource 动态选项  
  
### WQLQuerySource = 直接输入  
 **WQLQuerySource**  
 提供查询，或单击省略号按钮 (...) 并使用“WQL 查询”对话框输入查询。  
  
### WQLQuerySource = 文件连接  
 **WQLQuerySource**  
 在列表中选择一个文件连接管理器，或单击“\<新建连接…>”新建一个连接管理器。  
  
 **相关主题：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### WQLQuerySource = 变量  
 **WQLQuerySource**  
 从列表中选择变量，或单击“\<新建变量...>”以创建新的变量。  
  
 **相关主题：**[Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)、[添加变量](../Topic/Add%20Variable.md)  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [WMI 事件观察器任务编辑器（“常规”页）](../../integration-services/control-flow/wmi-event-watcher-task-editor-general-page.md)   
 [“表达式”页](../../integration-services/expressions/expressions-page.md)   
 [WMI 数据读取器任务](../../integration-services/control-flow/wmi-data-reader-task.md)  
  
  