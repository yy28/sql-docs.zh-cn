---
title: SMO 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.smoconnection.f1
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c69a68deb08cfd0248b9b27562a687a2ee10f939
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649977"
---
# <a name="smo-connection-manager"></a>SMO 连接管理器
  SMO 连接管理器使得包能够连接到 SQL 管理对象 (SMO) 服务器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括的传输任务使用 SMO 连接管理器。 例如，传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的传输登录任务使用 SMO 连接管理器。  
  
 将 SMO 连接管理器添加到包时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时决定 SMO 连接的连接管理器，设置该连接管理器的属性，并将该连接管理器添加到包上的“连接”集合。 该连接管理器的 **ConnectionManagerType** 属性设置为 **SMOServer**。  
  
 可以按下列方式配置 SMO 连接管理器：  
  
-   指定安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的服务器的名称。  
  
-   为连接到服务器选择身份验证模式。  
  
## <a name="configuration-of-the-smo-connection-manager"></a>SMO 连接管理器的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [SMO 连接管理器编辑器](../../integration-services/connection-manager/smo-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
## <a name="smo-connection-manager-editor"></a>SMO 连接管理器编辑器
  可以使用 **“SMO 连接管理器编辑器”** 配置各种传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象的任务使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接。  
  
 若要了解有关 SMO 连接管理器的详细信息，请参阅 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
### <a name="options"></a>选项  
 **服务器名称**  
 键入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称，或者从列表中选择服务器名称。  
  
 **“刷新”**  
 刷新网络可检测到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用实例的列表。  
  
 **Use Windows Authentication**  
 使用 Windows 身份验证连接所选的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
 **Use SQL Server Authentication**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证连接所选的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
 **User name**  
 如果选择了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，那么请输入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户名。  
  
 **密码**  
 如果选择了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，那么请输入密码。  
  
 **测试连接**  
 根据配置测试连接。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services (SSIS) 连接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
