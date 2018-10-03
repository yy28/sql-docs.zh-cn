---
title: SMTP 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a5ede293cf4965d89e333d1672a15de6811ec8d7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084947"
---
# <a name="smtp-connection-manager"></a>SMTP 连接管理器
  SMTP 连接管理器使包可以连接到简单邮件传输协议 (SMTP) 服务器。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的发送邮件任务使用 SMTP 连接管理器。  
  
 如果将 Microsoft Exchange 用作 SMTP 服务器，则可能需要配置 SMTP 连接管理器才能使用 Windows 身份验证。 Exchange 服务器可以配置为不支持未经身份验证的 SMTP 连接。  
  
## <a name="configuration-the-smtp-connection-manager"></a>SMTP 连接管理器的配置  
 当将一个 SMTP 连接管理器添加到包中，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]创建的连接管理器，将 SMTP 连接在运行时解析、 设置连接管理器属性，并将连接管理器`Connections`集合包。 `ConnectionManagerType`连接管理器属性设置为`SMTP`。  
  
 可以使用下列方式配置 SMTP 连接管理器：  
  
-   提供一个连接字符串。  
  
-   指定 SMTP 服务器的名称。  
  
-   指定要使用的身份验证方法。  
  
    > [!IMPORTANT]  
    >  SMTP 连接管理器仅支持匿名身份验证和 Windows 身份验证， 而不支持基本身份验证。  
  
-   指定在发送电子邮件时是否使用安全套接字层 (SSL) 对通信进行加密。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [SMTP 连接管理器编辑器](../smtp-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>并[连接以编程方式添加](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
  
