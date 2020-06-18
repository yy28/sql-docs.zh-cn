---
title: Web 服务任务编辑器（"输出" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 73c83969-7b0e-479d-a436-0a46b2068d01
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4b8dbb9847f3591d0f26a2dc7ca6e31f1b22da83
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972447"
---
# <a name="web-service-task-editor-output-page"></a>Web 服务任务编辑器（“输出”页）
  可以使用 **“Web 服务任务编辑器”** 对话框的 **“输出”** 页，指定 Web 方法返回的结果的存储位置。  
  
 若要了解此任务，请参阅 [Web 服务任务](control-flow/web-service-task.md)。  
  
## <a name="static-options"></a>静态选项  
 **OutputType**  
 选择存储结果时所使用的存储类型。 此属性具有下表所列的选项。  
  
|值|说明|  
|-----------|-----------------|  
|**文件连接**|将结果存储在文件中。 选择此值将显示动态选项 **File**。|  
|**变量**|将结果存储在变量中。 选择此值将显示动态选项 **Variable**。|  
  
## <a name="outputtype-dynamic-options"></a>OutputType 动态选项  
  
### <a name="outputtype--file-connection"></a>OutputType = 文件连接  
 **File**  
 在列表中选择一个文件连接管理器，或单击 " \<**New Connection...**> 新建连接管理器"。  
  
 **相关主题：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="outputtype--variable"></a>OutputType = 变量  
 **变量**  
 在列表中选择变量，或单击 \<**New Variable...**> 创建新变量。  
  
 **相关主题：**  [Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、[添加变量](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Web 服务任务编辑器 &#40;常规 "页面&#41;](general-page-of-integration-services-designers-options.md)   
 [Web 服务任务编辑器 &#40;输入页&#41;](../../2014/integration-services/web-service-task-editor-input-page.md)   
 [“表达式”页](expressions/expressions-page.md)  
  
  
