---
title: WMI 数据读取器任务编辑器（"WMI 选项" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WMI Data Reader Task Editor
ms.assetid: 4b8d4716-882d-41b0-b77e-e0e2741a2cd5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 08418775cc0b1f865d75cb07536a60956ea4ff0a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972397"
---
# <a name="wmi-data-reader-task-editor-wmi-options-page"></a>WMI 数据读取器任务编辑器（“WMI 选项”页）
  可以使用“WMI 数据读取器任务编辑器”**** 对话框的“WMI 选项”**** 页，指定 Windows Management Instrumentation 查询语言 (WQL) 查询的源和查询结果的目标。  
  
 若要了解此任务，请参阅 [WMI Data Reader Task](control-flow/wmi-data-reader-task.md)。 有关 WMI 查询语言 (WQL) 的详细信息，请参阅 MSDN 库中的 Windows Management Instrumentation 主题 [Querying with WQL](https://go.microsoft.com/fwlink/?LinkId=79045)（利用 WQL 进行查询）。  
  
## <a name="static-options"></a>静态选项  
 **WMIConnectionName**  
 在列表中选择一个 WMI 连接管理器，或单击 " \<**New WMI Connection...**> 新建连接管理器"。  
  
 **相关主题：** [WMI 连接管理器](connection-manager/wmi-connection-manager.md)和 [WMI 连接管理器编辑器](../../2014/integration-services/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 选择任务运行的 WQL 查询的源类型。 此属性具有下表所列的选项。  
  
|值|说明|  
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
  
|值|说明|  
|-----------|-----------------|  
|**文件连接**|选择用于保存 WQL 查询结果的文件。 选择此值将显示动态选项 **DestinationType**。|  
|**变量**|设置用于存储 WQL 查询结果的变量。 选择此值将显示动态选项 **DestinationType**。|  
  
## <a name="wqlquerysourcetype-dynamic-options"></a>WQLQuerySourceType 动态选项  
  
### <a name="wqlquerysourcetype--direct-input"></a>WQLQuerySourceType = 直接输入  
 **WQLQuerySource**  
 提供查询，或单击省略号（...），然后使用 " **WQL 查询**" 对话框输入查询。  
  
### <a name="wqlquerysourcetype--file-connection"></a>WQLQuerySourceType = 文件连接  
 **WQLQuerySource**  
 在列表中选择一个文件连接管理器，或单击 " \<**New connection...**> 新建连接管理器"。  
  
 **相关主题：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="wqlquerysourcetype--variable"></a>WQLQuerySourceType = 变量  
 **WQLQuerySource**  
 在列表中选择变量，或单击 \<**New variable...**> 创建新变量。  
  
 **相关主题：** [Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、[添加变量](../../2014/integration-services/add-variable.md)  
  
## <a name="destinationtype-dynamic-options"></a>DestinationType 动态选项  
  
### <a name="destinationtype--file-connection"></a>DestinationType = 文件连接  
 **目标**  
 在列表中选择一个文件连接管理器，或单击 " \<**New connection...**> 新建连接管理器"。  
  
 **相关主题：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="destinationtype--variable"></a>DestinationType = 变量  
 **目标**  
 在列表中选择变量，或单击 \<**New variable...**> 创建新变量。  
  
 **相关主题：** [Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、[添加变量](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [WMI 数据读取器任务编辑器 &#40;常规 "页面&#41;](general-page-of-integration-services-designers-options.md)   
 [表达式页](expressions/expressions-page.md)   
 [WMI 事件观察器任务](control-flow/wmi-event-watcher-task.md)  
  
  
