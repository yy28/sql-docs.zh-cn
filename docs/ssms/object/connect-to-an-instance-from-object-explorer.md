---
title: "从对象资源管理器连接到实例 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 53043981ec7d3d66f3a16252a5dd90a9ad323aa6
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-an-instance-from-object-explorer"></a>从对象资源管理器连接到实例
若要使用对象资源管理器管理对象，必须首先将对象资源管理器连接到包含对象的实例。 可以同时将对象资源管理器连接到多个实例。  
  
## <a name="connecting-object-explorer-to-a-server"></a>将对象资源管理器连接到服务器  
若要使用对象资源管理器，必须先将其连接到服务器上。 单击对象资源管理器工具栏上的“连接”，并从下拉列表中选择服务器的类型。 将打开“连接到服务器”对话框。 若要连接，您至少要提供服务器名称和正确的身份验证信息。  
  
## <a name="optional-object-explorer-connection-settings"></a>可选的对象资源管理器连接设置  
连接到服务器时，可以在“连接到服务器”对话框中指定其他连接信息。 “连接到服务器”对话框将保留上次使用的设置，新连接（例如新代码编辑器窗口）将使用这些设置。  
  
若要指定可选的连接设置，请遵循以下步骤：  
  
1.  单击对象资源管理器工具栏上的“连接”，并单击要连接到的服务器类型。 此时，将显示 **“连接到服务器”** 对话框。  
  
2.  在“服务器名称”框中，键入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 实例的名称。  
  
3.  单击“选项”。 “连接到服务器”对话框将显示其他选项。  
  
4.  单击“连接属性”选项卡以配置其他设置。 可用的设置因服务器类型而异。 下面是可用于 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的设置。  
  
    |设置|Description|  
    |-----------|---------------|  
    |**连接到数据库**|从服务器上的可用数据库中选择。 此列表只显示您具有查看权限的数据库。|  
    |**网络协议**|从 Shared Memory、TCP/IP 或 Named Pipes 中选择。|  
    |**网络数据包大小**|以字节为单位进行配置。 默认设置是 4096 字节。|  
    |**连接超时值**|以秒为单位进行配置。 默认值是 15 秒。|  
    |**执行超时值**|以秒为单位进行配置。 默认设置 (0) 表示执行永远不会超时。|  
    |**加密连接**|强制加密。|  
  
5.  若要将指定的服务器添加到已注册的服务器列表中，请单击“已注册的服务器”选项卡，并在希望显示新服务器的位置上单击，然后完成连接。  
  
> [!NOTE]  
> 使用“其他连接参数”页可以将更多连接参数添加到连接字符串。 有关详细信息，请参阅[连接到服务器（“其他连接参数”页）](../../ssms/f1-help/connect-to-server-additional-connection-parameters-page.md)。  
  

