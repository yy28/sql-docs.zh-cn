---
description: 传输错误消息任务
title: 传输错误消息任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfererrormessagestask.f1
- sql13.dts.designer.transfererrormessagestask.general.f1
- sql13.dts.designer.transfererrormessagestask.errormessages.F1
helpviewer_keywords:
- Transfer Error Messages task [Integration Services]
ms.assetid: da702289-035a-4d14-bd74-04461fbfee1b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa0bf307931b25b72a56e069e9f1c45b9e6c8b5d
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192777"
---
# <a name="transfer-error-messages-task"></a>传输错误消息任务

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  传输错误消息任务可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之间传输一个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用户定义错误消息。 用户定义的消息是标识符等于或大于 50000 的消息。 标识符小于 50000 的消息是系统错误消息，无法使用传输错误消息任务来传输它。  
  
 传输错误消息任务可以配置为传输所有错误消息，也可以配置为只传输指定的错误消息。 用户定义的错误消息可以多种不同的语言提供，该任务可以配置为只传输选定语言的消息。 对于使用代码页 1033 的 us_english 版本的消息来说，在可以将该消息的其他语言版本传输到目标服务器之前，此消息必须已存在于该服务器上。  
  
 master 数据库中的 sysmessages 表包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的所有错误消息，包括系统错误消息和用户定义的错误消息。  
  
 要传输的用户定义的消息可能已经存在于目标服务器上。 如果标识符和语言相同，则错误消息会被视为重复的错误消息。 传输错误消息任务可以配置为以下列方式处理现有错误消息：  
  
-   覆盖现有错误消息。  
  
-   如果存在重复消息，则该任务失败。  
  
-   跳过重复的错误消息。  
  
 在运行时，传输错误消息任务使用一个或多个 SMO 连接管理器连接到源服务器和目标服务器。 SMO 连接管理器与传输错误消息任务分开进行配置，然后在传输错误消息任务中引用连接管理器。 SMO 连接管理器指定服务器以及在访问该服务器时要使用的身份验证模式。 有关详细信息，请参阅 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
 传输错误消息任务支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 源和目标。 对于使用哪个版本作为源或目标，没有限制。  
  
## <a name="events"></a>事件  
 该任务引发一个报告已经传输的错误消息数的信息事件。  
  
 传输错误消息任务并不报告错误消息传输的进度，它仅报告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>执行值  
 在该任务的 **ExecutionValue** 属性中定义的执行值返回已传输的错误消息数。 通过将用户定义的变量分配给传输错误消息任务的 **ExecValueVariable** 属性，包中的其他对象就可以访问有关错误消息传输的信息。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)和[在包中使用变量](../integration-services-ssis-variables.md)。  
  
## <a name="log-entries"></a>日志项  
 传输错误消息任务包括下列自定义日志项：  
  
-   TransferErrorMessagesTaskStartTransferringObjects    此日志项报告传输已经开始。 日志项包括开始时间。  
  
-   TransferErrorMessagesTaskFinishedTransferringObjects   此日志项报告传输已经完成。 日志项包括结束时间。  
  
 此外， **OnInformation** 事件的日志项报告已传输的错误消息数， **OnWarning event** 的日志项是为目标服务器上被覆盖的每个错误消息写入的。  
  
## <a name="security-and-permissions"></a>安全和权限  
 若要新建错误消息，运行该包的用户必须是目标服务器上 sysadmin 的成员或 serveradmin 服务器角色。  
  
## <a name="configuration-of-the-transfer-error-messages-task"></a>配置传输错误消息任务  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
 有关以编程方式设置这些属性的信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferErrorMessagesTask.TransferErrorMessagesTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
## <a name="transfer-error-messages-task-editor-general-page"></a>传输错误消息任务编辑器（“常规”页）
  可以使用 **“传输错误消息任务编辑器”** 对话框的 **“常规”** 页，对传输错误消息任务进行命名和说明。 传输错误消息任务可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之间传输一个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用户定义错误消息。   
  
### <a name="options"></a>选项  
 **名称**  
 为传输错误消息任务键入唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **说明**  
 键入传输错误消息任务的说明。  
  
## <a name="transfer-error-messages-task-editor-messages-page"></a>传输错误消息任务编辑器（“消息”页）
  可以使用“传输错误消息任务编辑器”对话框的“消息”页指定属性，以将一个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户定义错误消息从一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例复制到另一个实例。 
  
### <a name="options"></a>选项  
 **SourceConnection**  
 从列表中选择一个 SMO 连接管理器，或单击 \<New connection...> 创建与源服务器的新连接。  
  
 **DestinationConnection**  
 从列表中选择一个 SMO 连接管理器，或单击 \<New connection...> 创建与目标服务器的新连接。  
  
 **IfObjectExists**  
 选择在目标服务器上已存在同名的错误消息时，该任务是应该覆盖现有的用户定义错误消息还是跳过现有消息，或是失败。  
  
 **TransferAllErrorMessages**  
 选择该任务应将全部用户定义消息还是只有指定的用户定义消息从源服务器复制到目标服务器。  
  
 此属性具有下表所列的选项：  
  
|值|说明|  
|-----------|-----------------|  
|**True**|复制所有用户定义消息。|  
|**False**|仅复制指定的用户定义消息。|  
  
 **ErrorMessagesList**  
 单击浏览按钮 (...) 以选择要复制的错误消息  。  
  
> [!NOTE]  
>  必须先指定 **SourceConnection** ，然后才能选择要复制的错误消息。  
  
 **ErrorMessageLanguagesList**  
 单击浏览按钮 (...) 以选择将用户定义的错误消息发送到目标服务器所使用的语言  。 在目标服务器上必须存在 us_english（代码页 1033）版本的消息，才能将其他语言版本的消息传输到目标服务器。  
  
> [!NOTE]  
>  必须先指定 **SourceConnection** ，然后才能选择要复制的错误消息。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 任务](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流](../../integration-services/control-flow/control-flow.md)  
  
