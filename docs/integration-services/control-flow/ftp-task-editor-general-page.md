---
title: "FTP 任务编辑器 （常规页） |Microsoft 文档"
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
- sql13.dts.designer.ftptask.general.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 28b46fdd-b04a-4f97-a99f-883f5735a6d9
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 224fb99641a4ac4482371c4b607da5b06bd50df8
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="ftp-task-editor-general-page"></a>FTP 任务编辑器（“常规”页）
  使用 **“FTP 任务编辑器”** 对话框的 **“常规”** 页可以指定连接到与任务通信的 FTP 服务器的 FTP 连接管理器。 您还可以命名和描述 FTP 任务。  
  
 若要了解此任务，请参阅 [FTP 任务](../../integration-services/control-flow/ftp-task.md)。  
  
## <a name="options"></a>选项  
 **FtpConnection**  
 选择一个现有的 FTP 连接管理器，或单击\<**新的连接...**> 若要创建连接管理器。  
  
> [!IMPORTANT]  
>  FTP 连接管理器仅支持匿名身份验证和基本身份验证， 而不支持 Windows 身份验证。  
  
 **相关主题**： [FTP Connection Manager](../../integration-services/connection-manager/ftp-connection-manager.md)、 [FTP Connection Manager Editor](../../integration-services/connection-manager/ftp-connection-manager-editor.md)  
  
 **StopOnFailure**  
 指示在 FTP 操作失败时是否终止 FTP 任务。  
  
 **名称**  
 为 FTP 任务提供唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **Description**  
 键入对 FTP 任务的说明。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [FTP 任务编辑器 &#40;文件传输页 &#41;](../../integration-services/control-flow/ftp-task-editor-file-transfer-page.md)   
 [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
  
