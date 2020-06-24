---
title: 配置管理的 WMI 提供程序
description: 了解用于配置管理的 WMI 提供程序如何使用 WMI 来管理 SQL Server 中的服务、服务器别名和客户端/服务器网络设置。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4795ee1d456e5f4b823c24fc1ad48e81c9d6541e
ms.sourcegitcommit: bf5e9cb3a2caa25d0a37f401b3806b7baa5adea8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2020
ms.locfileid: "85295430"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>了解用于配置管理的 WMI 提供程序
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供用于配置管理的 WMI 提供程序。 这样，您便可以使用 Windows Management Instrumentation (WMI) 来管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端和服务器网络设置以及服务器别名。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务、网络设置和别名由计算机的 root\Microsoft\SqlServer\ComputerManagement*nn*命名空间中的 WMI 对象表示。 与指定计算机上的 WMI 提供程序建立连接后，可以使用 WQL 或脚本撰写语言查询服务、网络设置和别名。  
  
 WMI 提供程序是一个实例提供程序。 它提供[WMI 类](../../relational-databases/wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md)的实例，并支持以下异步操作。  
  
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
  
 有关使用 WMI 提供程序进行配置管理的管理应用程序的示例，请参阅[将 WQL 和脚本语言与用于配置管理的 Wmi 提供程序结合使用](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)。  
  
 有关使用 WMI 提供程序的编程管理应用程序的详细信息，请参阅 .NET Framework SDK 中的 WMI 文档 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
## <a name="see-also"></a>另请参阅  
 [使用 WMI 提供程序进行配置管理](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [将 WQL 和脚本语言用于配置管理的 WMI 提供程序](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
