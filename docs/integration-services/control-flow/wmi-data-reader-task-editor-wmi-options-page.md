---
title: "WMI 数据读取器任务编辑器（“WMI 选项”页） | Microsoft Docs"
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
  - "sql13.dts.designer.wmidatareadertask.wmiquery.f1"
helpviewer_keywords: 
  - "WMI 数据读取器任务编辑器"
ms.assetid: 4b8d4716-882d-41b0-b77e-e0e2741a2cd5
caps.latest.revision: 40
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# WMI 数据读取器任务编辑器（“WMI 选项”页）
  可以使用“WMI 数据读取器任务编辑器”对话框的“WMI 选项”页，指定 Windows Management Instrumentation 查询语言 (WQL) 查询的源和查询结果的目标。  
  
 若要了解此任务，请参阅 [WMI Data Reader Task](../../integration-services/control-flow/wmi-data-reader-task.md)。 有关 WMI 查询语言 (WQL) 的详细信息，请参阅 MSDN 库中的 Windows Management Instrumentation 主题 [Querying with WQL](http://go.microsoft.com/fwlink/?LinkId=79045)（利用 WQL 进行查询）。  
  
## 静态选项  
 **WMIConnectionName**  
 在列表中选择一个 WMI 连接管理器，或单击“\<新建 WMI 连接…>”新建一个连接管理器。  
  
 **相关主题：**[WMI 连接管理器](../../integration-services/connection-manager/wmi-connection-manager.md)和 [WMI 连接管理器编辑器](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 选择任务运行的 WQL 查询的源类型。 此属性具有下表所列的选项。  
  
|“值”|Description|  
|-----------|-----------------|  
|**直接输入**|为 WQL 查询设置源。 选择此值将显示动态选项 **WQLQuerySourceType**。|  
|**文件连接**|选择包含 WQL 查询的文件。 选择此值将显示动态选项 **WQLQuerySourceType**。|  
|**变量**|将源设置为定义 WQL 查询的变量。 选择此值将显示动态选项 **WQLQuerySourceType**。|  
  
 **OutputType**  
 指定输出是数据表、属性值还是属性名称和值。  
  
 **OverwriteDestination**  
 指定是保留、覆盖还是追加到目标文件或变量中的原始数据。  
  
 **目标类型**  
 选择任务运行的 WQL 查询的目标类型。 此属性具有下表所列的选项。  
  
|“值”|Description|  
|-----------|-----------------|  
|**文件连接**|选择用于保存 WQL 查询结果的文件。 选择此值将显示动态选项 **DestinationType**。|  
|**变量**|设置用于存储 WQL 查询结果的变量。 选择此值将显示动态选项 **DestinationType**。|  
  
## WQLQuerySourceType 动态选项  
  
### WQLQuerySourceType = 直接输入  
 **WQLQuerySource**  
 提供查询，或单击省略号 (…)，然后使用“WQL 查询”对话框输入查询。  
  
### WQLQuerySourceType = 文件连接  
 **WQLQuerySource**  
 在列表中选择一个文件连接管理器，或单击“\<新建连接…>”新建一个连接管理器。  
  
 **相关主题：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### WQLQuerySourceType = 变量  
 **WQLQuerySource**  
 从列表中选择变量，或单击“\<新建变量...>”以创建新的变量。  
  
 **相关主题：**[Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)、[添加变量](../Topic/Add%20Variable.md)  
  
## DestinationType 动态选项  
  
### DestinationType = 文件连接  
 **目标**  
 在列表中选择一个文件连接管理器，或单击“\<新建连接…>”新建一个连接管理器。  
  
 **相关主题：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### DestinationType = 变量  
 **目标**  
 从列表中选择变量，或单击“\<新建变量...>”以创建新的变量。  
  
 **相关主题：**[Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)、[添加变量](../Topic/Add%20Variable.md)  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [WMI 数据读取器任务编辑器（“常规”页）](../../integration-services/control-flow/wmi-data-reader-task-editor-general-page.md)   
 [“表达式”页](../../integration-services/expressions/expressions-page.md)   
 [WMI 事件观察器任务](../../integration-services/control-flow/wmi-event-watcher-task.md)  
  
  