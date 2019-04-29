---
title: 消息队列任务编辑器 （发送页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msgqueuetask.send.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 565aa079-ac44-4407-8efc-cddab839de30
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e203bd95b4e3d42747614dc9aa688cc549338f19
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62890732"
---
# <a name="message-queue-task-editor-send-page"></a>消息队列任务编辑器（“发送”页）
  可以使用 **“消息队列任务编辑器”** 对话框的 **“发送”** 页，配置消息队列任务以便从 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包发送消息。  
  
 若要了解此任务，请参阅 [Message Queue Task](control-flow/message-queue-task.md)。  
  
## <a name="options"></a>选项  
 **UseEncryption**  
 指示是否对消息进行加密。 默认值为 `False`。  
  
 **EncryptionAlgorithm**  
 如果选择使用加密，请指定要使用的加密算法的名称。 消息队列任务可以使用 RC2 和 RC4 算法。 默认值为 **RC2**。  
  
> [!NOTE]  
>  RC4 算法仅用于支持向后兼容性。 仅当数据库兼容级别为 90 或 100 时，才能使用 RC4 或 RC4_128 对新材料进行加密。 （建议不要使用。）而是使用一种较新的算法，如 AES 算法之一。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的当前版本中，可以通过任何兼容级别对使用 RC4 或 RC4_128 加密的材料进行解密。  
  
> [!IMPORTANT]  
>  这些算法是消息队列（也称为 MSMQ）技术支持的加密算法。 与较新的算法相比，这两种加密算法都被视为加密性很弱的算法，但消息队列尚不支持新的算法。 因此，在使用消息队列任务发送消息时，应考虑您的加密需要。  
  
 **MessageType**  
 选择消息类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**数据文件消息**|消息存储在文件中。 选择该值将显示动态选项 **DataFileMessage**。|  
|**变量消息**|消息存储在变量中。 选择该值将显示动态选项 **VariableMessage**。|  
|**字符串消息**|消息存储在消息队列任务中。 选择该值将显示动态选项 **StringMessage**。|  
  
## <a name="messagetype-dynamic-options"></a>MessageType 动态选项  
  
### <a name="messagetype--data-file-message"></a>MessageType = 数据文件消息  
 **DataFileMessage**  
 键入数据文件的路径，或单击省略号 (…) 后再定位到相应的文件。  
  
### <a name="messagetype--variable-message"></a>MessageType = 变量消息  
 **VariableMessage**  
 键入变量名称，或单击省略号 (…) 后再选择相应的变量。 各变量之间用逗号分隔。  
  
 **相关主题：** 选择变量  
  
### <a name="messagetype--string-message"></a>MessageType = 字符串消息  
 **StringMessage**  
 键入字符串消息，或单击省略号 (…) 后在“输入字符串消息”对话框中键入消息。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [消息队列任务编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)   
 [消息队列任务编辑器（“接收”页）](../../2014/integration-services/message-queue-task-editor-receive-page.md)   
 [“表达式”页](expressions/expressions-page.md)  
  
  
