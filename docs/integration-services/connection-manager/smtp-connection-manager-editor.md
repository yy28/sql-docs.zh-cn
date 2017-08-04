---
title: "SMTP 连接管理器编辑器 |Microsoft 文档"
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
- sql13.dts.designer.smtpconnection.f1
helpviewer_keywords:
- SMTP Connection Manager Editor
ms.assetid: 2693de0d-b04d-4325-a856-ce667d2b8aa1
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3ef8edce1f187ac427463a0a0722c12666265d93
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="smtp-connection-manager-editor"></a>SMTP 连接管理器编辑器
  使用“SMTP 连接管理器编辑器”对话框可以指定简单邮件传输协议 (SMTP) 服务器。  
  
 若要了解有关 SMTP 连接管理器的详细信息，请参阅 [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md)。  
  
## <a name="options"></a>选项  
 **名称**  
 为连接管理器提供唯一的名称。  
  
 **Description**  
 描述连接管理器。 最好按照连接管理器的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
 **SMTP 服务器**  
 提供 SMTP 服务器的名称。  
  
 **使用 Windows 身份验证**  
 如果选中此选项，在通过 SMTP 服务器发送邮件时将使用 Windows 身份验证来验证对服务器的访问权限。  
  
> [!IMPORTANT]  
>  SMTP 连接管理器仅支持匿名身份验证和 Windows 身份验证， 而不支持基本身份验证。  
  
> [!NOTE]  
>  使用 Microsoft Exchange 作为 SMTP 服务器时，可能需要将 **“使用 Windows 身份验证”** 设置为 **True**。 Exchange 服务器可以配置为不支持未经身份验证的 SMTP 连接。  
  
 **启用安全套接字层 (SSL)**  
 如果选中此选项，则在发送电子邮件时，将使用安全套接字层 (SSL) 来加密通信。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)  
  
  
