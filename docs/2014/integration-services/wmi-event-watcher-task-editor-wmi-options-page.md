---
title: WMI 事件观察器任务编辑器 （WMI 选项页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmieventwatcher.wmiquery.f1
helpviewer_keywords:
- WMI Event Watcher Task Editor
ms.assetid: 525f3de7-a021-4e52-9939-3a83c88f131a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 52ca90b38975c8db762ec0937b265a91b03c5cb2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054374"
---
# <a name="wmi-event-watcher-task-editor-wmi-options-page"></a>WMI 事件观察器任务编辑器（“WMI 选项”页）
  可以使用“WMI 事件观察器任务编辑器”对话框的“WMI 选项”页，指定 Windows Management Instrumentation 查询语言 (WQL) 查询的源以及 WMI 事件观察器任务响应 Microsoft Windows Instrumentation (WMI) 事件的方式。  
  
 若要了解此任务，请参阅 [WMI Event Watcher Task](control-flow/wmi-event-watcher-task.md)。 有关 WMI 查询语言 (WQL) 的详细信息，请参阅 MSDN 库中的 Windows Management Instrumentation 主题 [Querying with WQL](https://go.microsoft.com/fwlink/?LinkId=79045)（利用 WQL 进行查询）。  
  
## <a name="static-options"></a>静态选项  
 **WMIConnectionName**  
 从列表中选择 WMI 连接管理器，或单击“\<新建 WMI 连接…>”，新建一个连接管理器。  
  
 **相关主题：**[WMI 连接管理器](connection-manager/wmi-connection-manager.md)、[WMI 连接管理器编辑器](../../2014/integration-services/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 选择任务运行的 WQL 查询的源类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接输入**|为 WQL 查询设置源。 选择此值将显示动态选项 **WQLQuerySource**。|  
|**文件连接**|选择包含 WQL 查询的文件。 选择此值将显示动态选项 **WQLQuerySource**。|  
|**变量**|将源设置为定义 WQL 查询的变量。 选择此值将显示动态选项 **WQLQuerySource**。|  
  
 **ActionAtEvent**  
 指定 WMI 事件是记录事件并启动 [!INCLUDE[ssIS](../includes/ssis-md.md)] 操作，还是只记录事件。  
  
 **AfterEvent**  
 指定任务在收到 WMI 事件之后是成功还是失败，或者任务是否继续监视事件的再次发生。  
  
 **ActionAtTimeout**  
 指定任务是记录 WMI 查询超时并启动 [!INCLUDE[ssIS](../includes/ssis-md.md)] 事件作为响应，还是只记录超时。  
  
 **AfterTimeout**  
 指定任务对超时的响应是成功还是失败，或者任务是否继续监视超时的再次发生。  
  
 **NumberOfEvents**  
 指定要监视的事件数。  
  
 **超时**  
 指定等待事件发生的秒数。 值为 0 表示实际上无超时。  
  
## <a name="wqlquerysource-dynamic-options"></a>WQLQuerySource 动态选项  
  
### <a name="wqlquerysource--direct-input"></a>WQLQuerySource = 直接输入  
 **WQLQuerySource**  
 提供查询，或单击省略号按钮 (...) 并使用“WQL 查询”对话框输入查询。  
  
### <a name="wqlquerysource--file-connection"></a>WQLQuerySource = 文件连接  
 **WQLQuerySource**  
 在列表中选择一个文件连接管理器，或单击“\<新建连接…>”新建一个连接管理器。  
  
 **相关主题：**[文件连接管理器](connection-manager/file-connection-manager.md)、[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="wqlquerysource--variable"></a>WQLQuerySource = 变量  
 **WQLQuerySource**  
 从列表中选择变量，或单击“\<新建变量...>”以创建新的变量。  
  
 **相关主题：**[Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、[添加变量](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [WMI 事件观察器任务编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)   
 [“表达式”页](expressions/expressions-page.md)   
 [WMI 数据读取器任务](control-flow/wmi-data-reader-task.md)  
  
  
