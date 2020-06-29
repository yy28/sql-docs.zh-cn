---
title: SMTP 连接管理器编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.smtpconnection.f1
helpviewer_keywords:
- SMTP Connection Manager Editor
ms.assetid: 2693de0d-b04d-4325-a856-ce667d2b8aa1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b303c15dbbad37a48b41ec73ed2c4baa461d5b13
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421324"
---
# <a name="smtp-connection-manager-editor"></a>SMTP 连接管理器编辑器
  使用“SMTP 连接管理器编辑器”  对话框可以指定简单邮件传输协议 (SMTP) 服务器。  
  
 若要了解有关 SMTP 连接管理器的详细信息，请参阅 [SMTP Connection Manager](connection-manager/smtp-connection-manager.md)。  
  
## <a name="options"></a>选项  
 **名称**  
 为连接管理器提供唯一的名称。  
  
 **说明**  
 描述连接管理器。 最好按照连接管理器的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
 **SMTP 服务器**  
 提供 SMTP 服务器的名称。  
  
 **Use Windows Authentication**  
 如果选中此选项，在通过 SMTP 服务器发送邮件时将使用 Windows 身份验证来验证对服务器的访问权限。  
  
> [!IMPORTANT]  
>  SMTP 连接管理器仅支持匿名身份验证和 Windows 身份验证， 而不支持基本身份验证。  
  
> [!NOTE]  
>  使用 Microsoft Exchange 作为 SMTP 服务器时，可能需要将 "**使用 Windows 身份验证**" 设置为 `True` 。 Exchange 服务器可以配置为不支持未经身份验证的 SMTP 连接。  
  
 **启用安全套接字层 (SSL)**  
 如果选中此选项，则在发送电子邮件时，将使用安全套接字层 (SSL) 来加密通信。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
