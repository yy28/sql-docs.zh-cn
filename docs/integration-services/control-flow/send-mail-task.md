---
title: "发送邮件任务 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sendmailtask.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: fd6f7a19c1b553ee06013a4a24fbbf26a759a6cd
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="send-mail-task"></a>发送邮件任务
  发送邮件任务可以发送电子邮件。 通过使用发送邮件任务，包可以在包工作流中的任务成功或失败时发送邮件，也可为响应运行时包引发的事件而发送邮件。 例如，该任务可以通知数据库管理员，告知备份数据库任务是成功还是失败。  
  
 可以采用下列方法配置发送邮件任务：  
  
-   提供电子邮件的消息正文。  
  
-   提供电子邮件的主题行。  
  
-   设置邮件的优先级别。 该任务支持三种优先级别：正常、低和高。  
  
-   在 To、Cc 和 Bcc 行中指定收件人。 如果任务指定多个收件人，则收件人之间用分号分隔。  
  
    > [!NOTE]  
    >  根据 Internet 标准，每个 To、Cc 和 Bcc 行最多包含 256 个字符。  
  
-   包含附件。 如果任务指定多个附件，则附件之间用管道符 (|) 分隔。  
  
    > [!NOTE]  
    >  如果包时运行时找不到附件文件，则将产生错误。  
  
-   指定要使用的 SMTP 连接管理器。  
  
    > [!IMPORTANT]  
    >  SMTP 连接管理器仅支持匿名身份验证和 Windows 身份验证， 而不支持基本身份验证。  
  
 消息正文可以是提供的字符串、包含文本的文件连接或包含文本的变量名。 该任务使用文件连接管理器来连接文件。 有关详细信息，请参阅 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)。  
  
 该任务使用 SMTP 连接管理器与邮件服务器建立连接。 有关详细信息，请参阅 [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md)。  
  
## <a name="custom-logging-messages-available-on-the-send-mail-task"></a>发送邮件任务可用的自定义日志记录消息  
 下表列出了发送邮件任务的自定义日志项。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|日志项|Description|  
|---------------|-----------------|  
|**SendMailTaskBegin**|指示任务开始发送电子邮件。|  
|**SendMailTaskEnd**|指示任务已发送完电子邮件。|  
|**SendMailTaskInfo**|提供有关任务的说明性信息。|  
  
## <a name="configuring-the-send-mail-task"></a>配置发送邮件任务  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的信息，请单击以下主题之一：  
  
-   [发送邮件任务编辑器（“常规”页）](../../integration-services/control-flow/send-mail-task-editor-general-page.md)  
  
-   [发送邮件任务编辑器（“邮件”页）](../../integration-services/control-flow/send-mail-task-editor-mail-page.md)  
  
-   [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
 有关以编程方式设置这些属性的信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>相关任务  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的信息，单击 [设置任务或容器的属性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)。  
  
## <a name="related-content"></a>相关内容  
  
-   shareourideas.com 上的技术文章 [How to send email with delivery notification in C#](http://go.microsoft.com/fwlink/?LinkId=237625)（如何在 C# 中发送具有传递通知的电子邮件）  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 任务](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流](../../integration-services/control-flow/control-flow.md)  
  
  
