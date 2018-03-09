---
title: "xp_cmdshell 服务器配置选项 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5bfdb40617fe5620854ff7c953736c63a2e31ca0
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="xpcmdshell-server-configuration-option"></a>xp_cmdshell 服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **xp_cmdshell** 选项是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器配置选项，该选项使系统管理员能够控制是否可以在系统上执行 **xp_cmdshell** 扩展存储过程。 新安装中默认禁用 xp_cmdshell 选项。 启用此选项前，请务必考虑使用此选项相关的潜在安全隐患。 新开发的代码不应使用此选项，因为它通常应处于禁用状态。 某些旧版应用程序需要启用此选项，如果不能将它们修改为避免使用此选项，可以使用基于策略的管理或运行 sp_configure 系统存储过程来启用此选项（如下面的代码示例所示）：  
  
```  
-- To allow advanced options to be changed.  
EXEC sp_configure 'show advanced options', 1;  
GO  
-- To update the currently configured value for advanced options.  
RECONFIGURE;  
GO  
-- To enable the feature.  
EXEC sp_configure 'xp_cmdshell', 1;  
GO  
-- To update the currently configured value for this feature.  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
