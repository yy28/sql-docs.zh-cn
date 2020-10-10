---
title: 使用 WQL 和脚本访问 WMI 提供程序
description: 了解如何通过使用 WQL 编辑器或查询工具或脚本语言，使用 WMI 提供程序访问 SQL Server 的服务和网络设置。
ms.custom: seo-lt-2019
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 52bc3bc300b1f6412ba2a4cdd3ce55ba5ca93aee
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891247"
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider"></a>通过 WMI 提供程序使用 WQL 和脚本语言
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  管理应用程序以两种方式使用针对配置管理对象的 Windows Management Instrumentation (WMI) 提供程序访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务和网络设置：  
  
-   使用某一 WQL 编辑器或查询工具（例如 WBEMTest.exe）可以查询通过 Windows Management Instrumentation 语言 (WQL) 设置的对象。  
  
-   使用某一脚本语言，例如 VBScript。  
  
 或者，可以使用 SMO 中的 WMI 托管对象以编程方式管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务和网络设置。 有关 WMI 托管对象编程的详细信息，请参阅 [使用 Wmi 提供程序管理服务和网络设置](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)。  
  
 可通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台访问用于配置管理的 WMI 提供程序。 有关从用户界面访问 WMI 提供程序的详细信息，请参阅 [管理服务操作指南主题 &#40;SQL Server 配置管理器&#41;](../../database-engine/configure-windows/scm-services-connect-to-another-computer.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用 WQL 访问用于配置管理的 WMI 提供程序](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-wql.md)   
 [使用 VBScript 访问 WMI 提供程序](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
