---
title: 使用 WQL 和脚本语言与 WMI 提供程序 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- scripts [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
- WMI Provider for Configuration Management, scripts
ms.assetid: c1e64905-3c2b-4974-88f4-abf17cf7e289
caps.latest.revision: 18
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: fd0c23313301ceefdc948ead21523b3710531c0f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider"></a>使用 WQL 和脚本语言与 WMI 提供程序
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  管理应用程序以两种方式使用针对配置管理对象的 Windows Management Instrumentation (WMI) 提供程序访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务和网络设置：  
  
-   使用某一 WQL 编辑器或查询工具（例如 WBEMTest.exe）可以查询通过 Windows Management Instrumentation 语言 (WQL) 设置的对象。  
  
-   使用某一脚本语言，例如 VBScript。  
  
 或者，可以使用 SMO 中的 WMI 托管对象以编程方式管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务和网络设置。 有关托管对象的编程 WMI 有关的详细信息，请参阅[管理服务和通过使用 WMI 提供程序的网络设置](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)。  
  
 可通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台访问用于配置管理的 WMI 提供程序。 有关从用户界面访问 WMI 提供程序的详细信息，请参阅[管理服务操作指南主题&#40;SQL Server 配置管理器&#41;](http://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6)。  
  
## <a name="see-also"></a>另请参阅  
 [访问 WMI 提供程序使用 WQL 的配置管理](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-wql.md)   
 [修改 SQL Server 服务高级属性使用 VBScript](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
  
