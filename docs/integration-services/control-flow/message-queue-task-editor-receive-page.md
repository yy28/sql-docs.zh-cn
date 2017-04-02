---
title: "消息队列任务编辑器（“接收”页） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.msgqueuetask.receive.f1"
helpviewer_keywords: 
  - "消息队列任务编辑器"
ms.assetid: 7028756d-1dcc-480c-bbcd-e9654f0772a0
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# 消息队列任务编辑器（“接收”页）
  可以使用“消息队列任务编辑器”对话框的“接收”页，配置消息队列任务以接收 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 消息队列 (MSMQ) 消息。  
  
 若要了解此任务，请参阅 [Message Queue Task](../../integration-services/control-flow/message-queue-task.md)。  
  
## 选项  
 **RemoveFromMessageQueue**  
 指示在接收后是否从队列中删除消息。 默认情况下，此值设置为 **False**。  
  
 **ErrorIfMessageTimeOut**  
 指示当消息超时时任务是否失败，并显示错误消息。 默认值为 **False**。  
  
 **TimeoutAfter**  
 如果选择任务失败时显示错误消息，则请指定显示超时消息之前等待的秒数。  
  
 **MessageType**  
 选择消息类型。 此属性具有下表所列的选项。  
  
|“值”|Description|  
|-----------|-----------------|  
|**数据文件消息**|消息存储在文件中。 选择该值将显示动态选项 **DataFileMessage**。|  
|**变量消息**|消息存储在变量中。 选择该值将显示动态选项 **VariableMessage**。|  
|**字符串消息**|消息存储在消息队列任务中。 选择该值将显示动态选项 **StringMessage**。|  
|**变量的字符串消息**|消息<br /><br /> 选择该值将显示动态选项 **StringMessage**。|  
  
## MessageType 动态选项  
  
### MessageType = 数据文件消息  
 **SaveFileAs**  
 键入要使用的文件的路径，或单击省略号按钮 **(…)**，然后查找该文件。  
  
 **Overwrite**  
 指示在保存数据文件消息的内容时是否覆盖现有文件中的数据。 默认值为 **False**。  
  
 **筛选**  
 指定是否对消息应用筛选器。 此属性具有下表所列的选项。  
  
|“值”|Description|  
|-----------|-----------------|  
|**无筛选器**|该任务不筛选消息。 选择该值将显示动态选项 **IdentifierReadOnly**。|  
|**来源包**|该消息仅接收来自指定包的消息。 选择该值将显示动态选项 **Identifier**。|  
  
### Filter 动态选项  
  
#### Filter = 无筛选器  
 **IdentifierReadOnly**  
 此选项是只读的。 如果以前设置了 Filter 属性，此选项可能为空或包含包的 GUID。  
  
#### Filter = 来源包  
 **Identifier**  
 如果选择应用筛选器，请键入可以从中接收消息的包的唯一标识符，或者单击省略号按钮 **(…)**，再指定包。  
  
 **相关主题：**[选择包](../../integration-services/control-flow/select-a-package.md)  
  
### MessageType = 变量消息  
 **筛选**  
 指定是否将筛选器应用到消息。 此属性具有下表所列的选项。  
  
|“值”|Description|  
|-----------|-----------------|  
|**无筛选器**|该任务不筛选消息。 选择该值将显示动态选项 **IdentifierReadOnly**。|  
|**来源包**|该消息仅接收来自指定包的消息。 选择该值将显示动态选项 **Identifier**。|  
  
 **变量**  
 键入变量名称，或单击“\<新建变量…>”，然后配置新的变量。  
  
 **相关主题：**[添加变量](../Topic/Add%20Variable.md)  
  
### Filter 动态选项  
  
#### Filter = 无筛选器  
 **IdentifierReadOnly**  
 此选项为空白。  
  
#### Filter = 来源包  
 **Identifier**  
 如果选择应用筛选器，请键入可以从中接收消息的包的唯一标识符，或者单击省略号按钮 **(…)**，再指定包。  
  
 **相关主题：**[选择包](../../integration-services/control-flow/select-a-package.md)  
  
### MessageType = 字符串消息  
 **比较**  
 指定是否将筛选器应用到消息。 此属性具有下表所列的选项。  
  
|“值”|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|不对消息进行比较。|  
|**Exact match**|消息必须与 **CompareString** 选项中的字符串完全匹配。|  
|**忽略大小写**|消息必须与 **CompareString** 选项中的字符串匹配，但在比较时不区分大小写。|  
|**包含**|消息必须包含 **CompareString** 选项中的字符串。|  
  
 **CompareString**  
 除非将 **Compare** 选项设置为“无”，否则请提供与消息进行比较的字符串。  
  
### MessageType = 变量的字符串消息  
 **比较**  
 指定是否将筛选器应用到消息。 此属性具有下表所列的选项。  
  
|“值”|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|不对消息进行比较。|  
|**Exact match**|消息必须与 **CompareString** 选项中的字符串完全匹配。|  
|**忽略大小写**|消息必须与 **CompareString** 选项中的字符串匹配，但在比较时不区分大小写。|  
|**包含**|消息必须包含 **CompareString** 选项中的字符串。|  
  
 **CompareString**  
 除非将 **Compare** 选项设置为“无”，否则请提供与消息进行比较的字符串。  
  
 **变量**  
 键入保存接收到的消息的变量名，或单击“\<新建变量…>”，然后配置新的变量。  
  
 **相关主题：**[添加变量](../Topic/Add%20Variable.md)  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [消息队列任务编辑器（“常规”页）](../../integration-services/control-flow/message-queue-task-editor-general-page.md)   
 [消息队列任务编辑器（“发送”页）](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [“表达式”页](../../integration-services/expressions/expressions-page.md)   
 [消息队列任务](../../integration-services/control-flow/message-queue-task.md)  
  
  