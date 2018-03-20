---
title: "了解的 WMI 提供程序的配置管理 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e31118f5df632d79ae5d1d098032ed2d1bcc33e4
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>了解用于配置管理的 WMI 提供程序
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供用于配置管理的 WMI 提供程序。 这样，您便可以使用 Windows Management Instrumentation (WMI) 来管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端和服务器网络设置以及服务器别名。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、 网络设置和别名由 WMI 对象中 root\Microsoft\SqlServer\ComputerManagement*nn*命名空间的计算机。 与指定计算机上的 WMI 提供程序建立连接后，可以使用 WQL 或脚本撰写语言查询服务、网络设置和别名。  
  
 WMI 提供程序是一个实例提供程序。 它会提供的实例[WMI 类](../../relational-databases/wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md)并支持下列异步操作。  
  
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
  
 有关管理应用程序使用的 WMI 提供程序的配置管理的示例，请参阅[使用 WQL 和脚本语言与 WMI 提供程序的配置管理](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)。  
  
 有关对管理应用程序使用 WMI 提供程序进行编程的详细信息，请参阅中的 WMI 文档[!INCLUDE[msCoName](../../includes/msconame-md.md)].NET Framework SDK。  
  
## <a name="see-also"></a>另请参阅  
 [使用的 WMI 提供程序的配置管理](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [使用 WQL 和脚本编写语言使用的 WMI 提供程序的配置管理](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
