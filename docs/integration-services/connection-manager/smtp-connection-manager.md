---
title: "SMTP 连接管理器 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: b952c9427a9bd15b29b806a5afb9f11d75d7393a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="smtp-connection-manager"></a>SMTP 连接管理器
  SMTP 连接管理器使包可以连接到简单邮件传输协议 (SMTP) 服务器。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的发送邮件任务使用 SMTP 连接管理器。  
  
 如果将 Microsoft Exchange 用作 SMTP 服务器，则可能需要配置 SMTP 连接管理器才能使用 Windows 身份验证。 Exchange 服务器可以配置为不支持未经身份验证的 SMTP 连接。  
  
## <a name="configuration-the-smtp-connection-manager"></a>SMTP 连接管理器的配置  
 将 SMTP 连接管理器添加到包时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时决定 SMTP 连接的连接管理器，设置该连接管理器的属性，并将该连接管理器添加到包的连接集合。 该连接管理器的 **ConnectionManagerType** 属性设置为 **SMTP**。  
  
 可以使用下列方式配置 SMTP 连接管理器：  
  
-   提供一个连接字符串。  
  
-   指定 SMTP 服务器的名称。  
  
-   指定要使用的身份验证方法。  
  
    > [!IMPORTANT]  
    >  SMTP 连接管理器仅支持匿名身份验证和 Windows 身份验证， 而不支持基本身份验证。  
  
-   指定在发送电子邮件时是否使用安全套接字层 (SSL) 对通信进行加密。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [SMTP 连接管理器编辑器](../../integration-services/connection-manager/smtp-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="smtp-connection-manager-editor"></a>SMTP 连接管理器编辑器
  使用“SMTP 连接管理器编辑器”对话框可以指定简单邮件传输协议 (SMTP) 服务器。  
  
 若要了解有关 SMTP 连接管理器的详细信息，请参阅 [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md)。  
  
### <a name="options"></a>选项  
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
  

