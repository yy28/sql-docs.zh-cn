---
title: 文件和版本号 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, versions
- components [SMO]
- files [SMO], components
- SMO [SQL Server], versions
- versions [SMO]
ms.assetid: 510907b6-e7a9-41bd-b892-d6d99a5118e1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0a1b0b28afbb83028af8d71644af08ca660a0b36
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62753409"
---
# <a name="files-and-version-numbers"></a>文件和版本号
  所有必需[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的管理对象（SMO）组件都作为[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端或服务器实例的一部分进行安装。 SMO 实现于几个托管程序集中。 您可以在客户端或服务器上开发 SMO 应用程序。  
  
|Directory|文件|说明|  
|---------------|----------|-----------------|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ConnectionInfo.dll|包含对连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的支持。|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ServiceBrokerEnum.dll|包含对编写 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker 的支持。 这仅在访问 Service Broker 的程序中是必需的。|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.Smo.dll|包含大多数 SMO 类。|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|包含对 SMO 类的支持。|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.WmiEnum.dll|包含 Windows Management Instrumentation (WMI) 提供程序类。 这仅对使用 WMI 提供程序类的程序是必需的。|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.RegSvrEnum.dll|包含注册服务器类。 这仅对使用注册服务器类的程序是必需的。|  
  
  
