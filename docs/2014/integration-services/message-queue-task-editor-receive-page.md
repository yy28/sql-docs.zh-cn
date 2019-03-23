---
title: 消息队列任务编辑器 （接收页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msgqueuetask.receive.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 7028756d-1dcc-480c-bbcd-e9654f0772a0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f2eec4fbeb300ce2a43e1007245fad573f1c5a44
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58387105"
---
# <a name="message-queue-task-editor-receive-page"></a>消息队列任务编辑器（“接收”页）
  可以使用“消息队列任务编辑器”对话框的“接收”页，配置消息队列任务以接收 [!INCLUDE[msCoName](../includes/msconame-md.md)] 消息队列 (MSMQ) 消息。  
  
 若要了解此任务，请参阅 [Message Queue Task](control-flow/message-queue-task.md)。  
  
## <a name="options"></a>选项  
 **RemoveFromMessageQueue**  
 指示在接收后是否从队列中删除消息。 默认情况下，此值设置为 `False`。  
  
 **ErrorIfMessageTimeOut**  
 指示当消息超时时任务是否失败，并显示错误消息。 默认值为 `False`。  
  
 **TimeoutAfter**  
 如果选择任务失败时显示错误消息，则请指定显示超时消息之前等待的秒数。  
  
 **MessageType**  
 选择消息类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**数据文件消息**|消息存储在文件中。 选择该值将显示动态选项 **DataFileMessage**。|  
|**变量消息**|消息存储在变量中。 选择该值将显示动态选项 **VariableMessage**。|  
|**字符串消息**|消息存储在消息队列任务中。 选择该值将显示动态选项 **StringMessage**。|  
|**变量的字符串消息**|消息<br /><br /> 选择该值将显示动态选项 **StringMessage**。|  
  
## <a name="messagetype-dynamic-options"></a>MessageType 动态选项  
  
### <a name="messagetype--data-file-message"></a>MessageType = 数据文件消息  
 **SaveFileAs**  
 键入要使用的文件的路径，或单击省略号按钮 (…) 后再定位到该文件。  
  
 **Overwrite**  
 指示在保存数据文件消息的内容时是否覆盖现有文件中的数据。 默认值为 `False`。  
  
 **Filter**  
 指定是否对消息应用筛选器。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**无筛选器**|该任务不筛选消息。 选择该值将显示动态选项 **IdentifierReadOnly**。|  
|**来源包**|该消息仅接收来自指定包的消息。 选择该值将显示动态选项 **Identifier**。|  
  
### <a name="filter-dynamic-options"></a>Filter 动态选项  
  
#### <a name="filter--no-filter"></a>Filter = 无筛选器  
 **IdentifierReadOnly**  
 此选项是只读的。 如果以前设置了 Filter 属性，此选项可能为空或包含包的 GUID。  
  
#### <a name="filter--from-package"></a>Filter = 来源包  
 **Identifier**  
 如果选择应用筛选器，请键入可以从中接收消息的包的唯一标识符，或者单击省略号按钮 (…)，再指定包。  
  
 **相关主题：**[选择包](control-flow/select-a-package.md)  
  
### <a name="messagetype--variable-message"></a>MessageType = 变量消息  
 **Filter**  
 指定是否将筛选器应用到消息。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**无筛选器**|该任务不筛选消息。 选择该值将显示动态选项 **IdentifierReadOnly**。|  
|**来源包**|该消息仅接收来自指定包的消息。 选择该值将显示动态选项 **Identifier**。|  
  
 **变量**  
 键入变量名称，或单击“\<新建变量…>”，然后配置新的变量。  
  
 **相关主题：**[添加变量](../../2014/integration-services/add-variable.md)  
  
### <a name="filter-dynamic-options"></a>Filter 动态选项  
  
#### <a name="filter--no-filter"></a>Filter = 无筛选器  
 **IdentifierReadOnly**  
 此选项为空白。  
  
#### <a name="filter--from-package"></a>Filter = 来源包  
 **Identifier**  
 如果选择应用筛选器，请键入可以从中接收消息的包的唯一标识符，或者单击省略号按钮 (…)，再指定包。  
  
 **相关主题：**[选择包](control-flow/select-a-package.md)  
  
### <a name="messagetype--string-message"></a>MessageType = 字符串消息  
 **比较**  
 指定是否将筛选器应用到消息。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|不对消息进行比较。|  
|**Exact match**|消息必须与 **CompareString** 选项中的字符串完全匹配。|  
|**忽略大小写**|消息必须与 **CompareString** 选项中的字符串匹配，但在比较时不区分大小写。|  
|**包含**|消息必须包含 **CompareString** 选项中的字符串。|  
  
 **CompareString**  
 除非将 **Compare** 选项设置为“无”，否则请提供与消息进行比较的字符串。  
  
### <a name="messagetype--string-message-to-variable"></a>MessageType = 变量的字符串消息  
 **比较**  
 指定是否将筛选器应用到消息。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|不对消息进行比较。|  
|**Exact match**|消息必须与 **CompareString** 选项中的字符串完全匹配。|  
|**忽略大小写**|消息必须与 **CompareString** 选项中的字符串匹配，但在比较时不区分大小写。|  
|**包含**|消息必须包含 **CompareString** 选项中的字符串。|  
  
 **CompareString**  
 除非将 **Compare** 选项设置为“无”，否则请提供与消息进行比较的字符串。  
  
 **变量**  
 键入保存接收到的消息的变量名，或单击“\<新建变量…>”，然后配置新的变量。  
  
 **相关主题：**[添加变量](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [消息队列任务编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)   
 [消息队列任务编辑器（“发送”页）](../../2014/integration-services/message-queue-task-editor-send-page.md)   
 [“表达式”页](expressions/expressions-page.md)   
 [Message Queue Task](control-flow/message-queue-task.md)  
  
  
