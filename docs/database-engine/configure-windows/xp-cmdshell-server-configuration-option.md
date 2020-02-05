---
title: xp_cmdshell 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 40efe03850259a3b900375e3a47c12d80a448b39
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68040071"
---
# <a name="xp_cmdshell-server-configuration-option"></a>xp_cmdshell 服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **xp_cmdshell** 选项是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器配置选项，该选项使系统管理员能够控制是否可以在系统上执行 **xp_cmdshell** 扩展存储过程。 新安装中默认禁用 xp_cmdshell 选项  。 启用此选项前，请务必考虑使用此选项相关的潜在安全隐患。 新开发的代码不应使用此选项，因为它通常应处于禁用状态。 某些旧版应用程序需要启用此选项，如果不能将它们修改为避免使用此选项，可以使用基于策略的管理或运行 sp_configure 系统存储过程来启用此选项（如下面的代码示例所示）  ：  
  
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
  
  
