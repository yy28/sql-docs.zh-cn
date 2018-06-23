---
title: FTP 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FTP connection manager
- connections [Integration Services], FTP
- connection managers [Integration Services], FTP
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5e96a1a11651106cd0534ec20a3a35b79a9f1e7e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129313"
---
# <a name="ftp-connection-manager"></a>FTP 连接管理器
  FTP 连接管理器使得包可以连接到文件传输协议 (FTP) 服务器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的 FTP 任务使用此连接管理器。  
  
 将 FTP 连接管理器添加到包时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建可以在运行时决定 FTP 连接的连接管理器，设置该连接管理器的属性，并将该连接管理器添加到包中的 `Connections` 集合。  
  
 `ConnectionManagerType`的连接管理器的属性设置为`FTP`。  
  
 可以按照下列方式配置 FTP 连接管理器：  
  
-   指定服务器名称和服务器端口。  
  
-   指定采用匿名访问，或者提供用户名和密码以进行基本身份验证。  
  
    > [!IMPORTANT]  
    >  FTP 连接管理器仅支持匿名身份验证和基本身份验证， 而不支持 Windows 身份验证。  
  
-   设置超时值、重试次数和可以一次复制的数据量。  
  
-   指示 FTP 连接管理器使用被动还是主动模式。  
  
 取决于与 FTP 连接管理器连接的 FTP 站点的配置，可能需要更改连接管理器的以下默认值：  
  
-   服务器端口设置为 21。 应当指定 FTP 站点侦听的端口。  
  
-   用户名设置为“anonymous”。 应当提供 FTP 站点需要的凭据。  
  
## <a name="activepassive-modes"></a>主动/被动模式  
 FTP 连接管理器可以使用主动模式或被动模式发送和接收文件。 在主动模式下，由服务器初始化数据连接；而在被动模式下，由客户端初始化数据连接。  
  
## <a name="configuration-of-the-ftp-connection-manager"></a>FTP 连接管理器的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的信息，请参阅 [TP 连接管理器编辑器](../ftp-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>和[添加连接以编程方式](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>请参阅  
 [FTP 任务](../control-flow/ftp-task.md)   
 [Integration Services &#40;SSIS&#41;连接](integration-services-ssis-connections.md)  
  
  