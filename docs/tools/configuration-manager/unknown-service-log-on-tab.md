---
title: 未知的服务 （在选项卡上的日志） |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e9b35cb5-d8ae-42ea-b59e-deedc99c4823
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 185860aebed7bab3df97af5199f5e2176594c56f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="unknown-service-log-on-tab"></a>未知服务（“登录”选项卡）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器无法识别此服务。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器从运行此服务的计算机上的 WMI 提供程序接收服务信息。 读取服务属性时出错，或者服务属性不完整。 若要解决此问题，请尝试关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器并将其重新打开，或者检查运行此服务的计算机上的 WMI 提供程序。  
  
 WMI 提供程序是 Windows 组件。 有关如何检查对 WMI 提供程序的权限的信息，请参阅 SQL Server 联机丛书中的“如何在 SQL Server 工具中将 WMI 配置为显示服务器状态”。  
  
 如果您认为自己查看的服务是正确的，请使用 **“未知服务属性”** 对话框中的 **“登录”** 选项卡，指定此服务使用的帐户，以及启动和停止此服务。  
  
## <a name="options"></a>“常规”  
 **本地系统帐户**  
 指定一个不要求输入密码的本地系统帐户。 但是，本地系统帐户可能会阻止该服务与其他服务器进行交互，具体取决于该帐户所拥有的权限。  
  
 **本帐户**  
 指定一个使用 Windows 身份验证的本地用户帐户或域用户帐户。 建议使用具有最低服务权限的域用户帐户。 有关选择帐户的信息，请参阅 SQL Server 联机丛书中的“设置 Windows 服务帐户”。  
  
 **帐户名**  
 指定本地用户帐户名或域用户帐户名。  
  
 **密码**  
 键入帐户的密码。  
  
 **确认密码**  
 再次键入帐户的密码。  
  
 **开始**  
 启动服务。  
  
 **停止**  
 停止服务。  
  
 **暂停**  
 暂停服务。  
  
 **恢复**  
 恢复暂停的服务。  
  
  
