---
title: "发送邮件任务编辑器（“邮件”页） | Microsoft Docs"
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
  - "sql13.dts.designer.sendmailtask.mail.f1"
helpviewer_keywords: 
  - "发送邮件任务编辑器"
ms.assetid: adb385d5-ef24-4d18-b9ea-b39e00a7075e
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# 发送邮件任务编辑器（“邮件”页）
  使用 **“发送邮件任务编辑器”** 对话框中的 **“邮件”** 页，可以指定收件人、邮件类型和邮件的优先级。 您还可以在邮件中附加文件。 邮件正文可以是您提供的字符串，也可以是指向包含文本的文件连接，还可以是包含文本的变量的名称。  
  
 若要了解此任务，请参阅 [Send Mail Task](../../integration-services/control-flow/send-mail-task.md)。  
  
## 选项  
 **SMTPConnection**  
 从列表中选择一个 SMTP 连接管理器，或单击“\<新建连接…>”创建新的连接管理器。  
  
> [!IMPORTANT]  
>  SMTP 连接管理器仅支持匿名身份验证和 Windows 身份验证， 而不支持基本身份验证。  
  
 **相关主题：**[SMTP 连接管理器](../../integration-services/connection-manager/smtp-connection-manager.md)  
  
 **From**  
 指定发件人的电子邮件地址。  
  
 **若要**  
 提供收件人的电子邮件地址，用分号分隔。  
  
 **抄送**  
 指定也可以收到邮件副本的各个人员的电子邮件地址，用分号分隔。  
  
 **密件抄送**  
 指定将收到邮件的隐蔽副本 (Bcc) 的各个人员的电子邮件地址，用分号分隔。  
  
 **主题**  
 提供电子邮件的主题。  
  
 **MessageSourceType**  
 选择消息的源类型。 此属性具有下表所列的选项。  
  
|“值”|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为邮件正文。 选择此值将显示动态选项 **MessageSource**。|  
|**文件连接**|将源设置为包含邮件正文的文件。 选择此值将显示动态选项 **MessageSource**。|  
|**变量**|将源设置为包含消息正文的变量。 选择此值将显示动态选项 **MessageSource**。|  
  
 **Priority**  
 设置邮件的优先级。  
  
 **Attachments**  
 为电子邮件附件提供文件名，用竖线 (|) 字符分隔。  
  
> [!NOTE]  
>  根据 Internet 标准，每个 To、Cc 和 Bcc 行最多包含 256 个字符。  
  
## MessageSourceType 动态选项  
  
### MessageSourceType = 直接输入  
 **MessageSource**  
 键入邮件正文，或单击“浏览(…)”按钮，然后在“消息源”对话框中键入邮件内容。  
  
### MessageSourceType = 文件连接  
 **MessageSource**  
 在列表中选择一个文件连接管理器，或单击\<“新建连接…”>新建一个连接管理器。  
  
 **相关主题：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### MessageSourceType = 变量  
 **MessageSource**  
 从列表中选择变量，或单击“新建变量...”以创建新的变量。  
  
 **相关主题：**[Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)、[添加变量](../Topic/Add%20Variable.md)  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [发送邮件任务编辑器（“常规”页）](../../integration-services/control-flow/send-mail-task-editor-general-page.md)   
 [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
  