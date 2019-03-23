---
title: FTP 任务编辑器 （常规页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftptask.general.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 28b46fdd-b04a-4f97-a99f-883f5735a6d9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1b64b1f8511c9d079118881a9862eee11fdb636d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388735"
---
# <a name="ftp-task-editor-general-page"></a>FTP 任务编辑器（“常规”页）
  使用 **“FTP 任务编辑器”** 对话框的 **“常规”** 页可以指定连接到与任务通信的 FTP 服务器的 FTP 连接管理器。 您还可以命名和描述 FTP 任务。  
  
 若要了解此任务，请参阅 [FTP 任务](control-flow/ftp-task.md)。  
  
## <a name="options"></a>选项  
 **FtpConnection**  
 选择现有 FTP 连接管理器，或单击“\<新建连接...>”以创建连接管理器。  
  
> [!IMPORTANT]  
>  FTP 连接管理器仅支持匿名身份验证和基本身份验证， 而不支持 Windows 身份验证。  
  
 **相关主题**：[FTP 连接管理器](connection-manager/ftp-connection-manager.md)、[FTP 连接管理器编辑器](../../2014/integration-services/ftp-connection-manager-editor.md)  
  
 **StopOnFailure**  
 指示在 FTP 操作失败时是否终止 FTP 任务。  
  
 **名称**  
 为 FTP 任务提供唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **说明**  
 键入对 FTP 任务的说明。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [FTP 任务编辑器（“文件传输”页）](../../2014/integration-services/ftp-task-editor-file-transfer-page.md)   
 [“表达式”页](expressions/expressions-page.md)  
  
  
