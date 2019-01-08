---
title: 了解配置管理的 WMI 提供程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b224868d4d9fc111cdbf9482282767420b6adcc8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52794689"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>了解用于配置管理的 WMI 提供程序
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供配置管理的 WMI 提供程序。 这样，您便可以使用 Windows Management Instrumentation (WMI) 来管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端和服务器网络设置以及服务器别名。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、 网络设置和别名由 root\Microsoft\SqlServer\ComputerManagement 中的 WMI 对象表示*nn*命名空间的计算机。 与指定计算机上的 WMI 提供程序建立连接后，可以使用 WQL 或脚本撰写语言查询服务、网络设置和别名。  
  
 WMI 提供程序是一个实例提供程序。 它提供的实例[WMI 类](../wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md)并支持以下异步操作。  
  
 实例检索  
 检索特定的类类型实例。  
  
 枚举  
 枚举类类型的所有实例。  
  
 修改  
 修改类类型的特定实例。  
  
 类具有用于修改其属性的方法。  
  
 删除  
 删除类类型的特定实例。  
  
 查询处理  
 根据筛选器枚举类类型的实例。  
  
 有关管理应用程序将用于配置管理的 WMI 提供程序的示例，请参阅[使用 WQL 和脚本语言的配置管理的 WMI 提供程序](using-wql-and-scripting-languages-with-the-wmi-provider.md)。  
  
 有关如何管理应用程序使用 WMI 提供程序进行编程的详细信息，请参阅中的 WMI 文档[!INCLUDE[msCoName](../../includes/msconame-md.md)].NET Framework SDK。  
  
## <a name="see-also"></a>请参阅  
 [使用配置管理的 WMI 提供程序](working-with-the-wmi-provider-for-configuration-management.md)   
 [将 WQL 和脚本语言用于配置管理的 WMI 提供程序](using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
