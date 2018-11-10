---
title: 使用 WQL 和脚本语言与 WMI 提供程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 8caf413d437817f8723403ff94c0864b3cd03ade
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51215095"
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider"></a>通过 WMI 提供程序使用 WQL 和脚本语言
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  管理应用程序以两种方式使用针对配置管理对象的 Windows Management Instrumentation (WMI) 提供程序访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务和网络设置：  
  
-   使用某一 WQL 编辑器或查询工具（例如 WBEMTest.exe）可以查询通过 Windows Management Instrumentation 语言 (WQL) 设置的对象。  
  
-   使用某一脚本语言，例如 VBScript。  
  
 或者，可以使用 SMO 中的 WMI 托管对象以编程方式管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务和网络设置。 有关托管对象的有关对 WMI 进行编程的详细信息，请参阅[管理服务和通过使用 WMI 提供程序的网络设置](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)。  
  
 可通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台访问用于配置管理的 WMI 提供程序。 有关从用户界面访问 WMI 提供程序的详细信息，请参阅[管理服务操作指南主题&#40;SQL Server 配置管理器&#41;](http://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6)。  
  
## <a name="see-also"></a>请参阅  
 [用于配置管理使用 WQL 访问 WMI 提供程序](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-wql.md)   
 [使用 VBScript 修改 SQL Server 服务高级属性](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
  
