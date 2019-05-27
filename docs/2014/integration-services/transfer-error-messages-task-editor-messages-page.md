---
title: 传输错误消息任务编辑器 （消息页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfererrormessagestask.errormessages.F1
helpviewer_keywords:
- Transfer Error Messages Task Editor
ms.assetid: cb2226a0-3037-4fdf-966f-81eabc0da9cf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f753aaddbd2647b1d8874b0d34db415f75aa99b9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66055041"
---
# <a name="transfer-error-messages-task-editor-messages-page"></a>传输错误消息任务编辑器（“消息”页）
  可以使用“传输错误消息任务编辑器”对话框的“消息”页指定属性，以将一个或多个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用户定义错误消息从一个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例复制到另一个实例。 有关此任务的详细信息，请参阅 [Transfer Error Messages Task](control-flow/transfer-error-messages-task.md)。  
  
## <a name="options"></a>选项  
 **SourceConnection**  
 从列表中选择 SMO 连接管理器，或单击“\<新建连接...>”，创建与源服务器的新连接。  
  
 **DestinationConnection**  
 从列表中选择 SMO 连接管理器，或单击“\<新建连接...>”，创建与目标服务器的新连接。  
  
 **IfObjectExists**  
 选择在目标服务器上已存在同名的错误消息时，该任务是应该覆盖现有的用户定义错误消息还是跳过现有消息，或是失败。  
  
 **TransferAllErrorMessages**  
 选择该任务应将全部用户定义消息还是只有指定的用户定义消息从源服务器复制到目标服务器。  
  
 此属性具有下表所列的选项：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**True**|复制所有用户定义消息。|  
|**False**|仅复制指定的用户定义消息。|  
  
 **ErrorMessagesList**  
 单击浏览按钮 (...) 以选择要复制的错误消息。  
  
> [!NOTE]  
>  必须先指定 **SourceConnection** ，然后才能选择要复制的错误消息。  
  
 **ErrorMessageLanguagesList**  
 单击浏览按钮 (...) 以选择将用户定义的错误消息发送到目标服务器所使用的语言。 在目标服务器上必须存在 us_english（代码页 1033）版本的消息，才能将其他语言版本的消息传输到目标服务器。  
  
> [!NOTE]  
>  必须先指定 **SourceConnection** ，然后才能选择要复制的错误消息。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 任务](control-flow/integration-services-tasks.md)   
 [传输错误消息任务编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)   
 [SMO 连接管理器](connection-manager/smo-connection-manager.md)   
 [传输错误消息任务编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)   
 [SMO 连接管理器](connection-manager/smo-connection-manager.md)  
  
  
