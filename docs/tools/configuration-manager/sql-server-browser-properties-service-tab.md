---
title: "SQL Server 浏览器属性 （服务选项卡） |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98ace9b0-72d5-4b72-9b7b-11fbc490981a
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8543b2ba7e1d9de73e31a93f1740a18be1671f5d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-browser-properties-service-tab"></a>SQL Server 浏览器属性（“服务”选项卡）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]浏览器程序作为服务运行在服务器上。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 浏览器侦听对 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源的传入请求，并提供计算机上安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的相关信息。  
  
 使用 **“SQL Server 浏览器属性”** 对话框中的 **“服务”** 选项卡可以查看下列选项。 除了 **“启动模式”** 以外，其他所有属性都是只读的。  
  
## <a name="options"></a>选项  
 **二进制路径**  
 显示此服务所使用的程序文件的位置。  
  
 **错误控制**  
 1 指示 `SERVICE_ERROR_NORMAL`。 如果在计算机启动过程中无法启动该服务，则启动程序会记录该错误并显示一个弹出消息框，但仍会继续执行启动操作。 此值不能更改。  
  
 **退出代码**  
 当发生错误时，错误号显示在此信息框中。 您可以通过在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知识库中搜索该号码获取相关信息来排除故障，或将该错误号提供给技术支持人员以获得帮助。  
  
 **Host Name**  
 显示运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务的计算机或群集的名称。  
  
 **名称**  
 指示该服务的显示名称。  
  
 **进程 ID**  
 显示 Windows 进程 ID。  
  
 **服务类型**  
 显示用于调用进程的服务的类型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装有多种服务。  
  
 **启动模式**  
 对此服务设置以下选项：  
  
-   手动：计算机启动时，此服务不自动启动。 您必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器或其他工具来启动该服务。  
  
-   自动：计算机启动时，此服务将尝试启动。  
  
-   已禁用：此服务无法启动。  
  
 **State**  
 指示此服务是正在运行、已停止还是已禁用。 **“...”**指示状态更改被挂起。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Browser 服务](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  
