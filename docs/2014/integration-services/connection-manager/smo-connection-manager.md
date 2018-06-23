---
title: SMO 连接管理器 | Microsoft Docs
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
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2202cb3f505dc17dfd9f1bcd283c36ca78ef02d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016885"
---
# <a name="smo-connection-manager"></a>SMO 连接管理器
  SMO 连接管理器使得包能够连接到 SQL 管理对象 (SMO) 服务器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括的传输任务使用 SMO 连接管理器。 例如，传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的传输登录任务使用 SMO 连接管理器。  
  
 当将 SMO 连接管理器添加到包，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]创建连接管理器，它将解析为 SMO 连接在运行时，设置连接管理器属性，并将添加到连接管理器`Connections`上的集合包。 `ConnectionManagerType`的连接管理器的属性设置为`SMOServer`。  
  
 可以按下列方式配置 SMO 连接管理器：  
  
-   指定安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的服务器的名称。  
  
-   为连接到服务器选择身份验证模式。  
  
## <a name="configuration-of-the-smo-connection-manager"></a>SMO 连接管理器的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [SMO 连接管理器编辑器](../smo-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>和[添加连接以编程方式](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services &#40;SSIS&#41;连接](integration-services-ssis-connections.md)  
  
  