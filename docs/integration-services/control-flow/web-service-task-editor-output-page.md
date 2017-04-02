---
title: "Web 服务任务编辑器（“输出”页） | Microsoft Docs"
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
  - "sql13.dts.designer.webservicestask.output.f1"
helpviewer_keywords: 
  - "Web 服务任务编辑器"
ms.assetid: 73c83969-7b0e-479d-a436-0a46b2068d01
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Web 服务任务编辑器（“输出”页）
  可以使用 **“Web 服务任务编辑器”** 对话框的 **“输出”** 页，指定 Web 方法返回的结果的存储位置。  
  
 若要了解此任务，请参阅 [Web 服务任务](../../integration-services/control-flow/web-service-task.md)。  
  
## 静态选项  
 **OutputType**  
 选择存储结果时所使用的存储类型。 此属性具有下表所列的选项。  
  
|“值”|Description|  
|-----------|-----------------|  
|**文件连接**|将结果存储在文件中。 选择此值将显示动态选项 **File**。|  
|**变量**|将结果存储在变量中。 选择此值将显示动态选项 **Variable**。|  
  
## OutputType 动态选项  
  
### OutputType = 文件连接  
 **文件**  
 在列表中选择一个文件连接管理器，或单击“\<新建连接…>”新建一个连接管理器。  
  
 **相关主题：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### OutputType = 变量  
 **变量**  
 从列表中选择变量，或单击“\<新建变量>...”以创建新的变量。  
  
 **相关主题：**[Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)、[添加变量](../Topic/Add%20Variable.md)  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [Web 服务任务编辑器（“常规”页）](../../integration-services/control-flow/web-service-task-editor-general-page.md)   
 [Web 服务任务编辑器（“输入”页）](../../integration-services/control-flow/web-service-task-editor-input-page.md)   
 [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
  