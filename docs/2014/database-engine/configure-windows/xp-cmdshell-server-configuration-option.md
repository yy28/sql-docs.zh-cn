---
title: xp_cmdshell 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: a7feec1765cf6ffaa3e46a300a5155ae73fb13db
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934688"
---
# <a name="xp_cmdshell-server-configuration-option"></a>xp_cmdshell 服务器配置选项
  **xp_cmdshell** 选项是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器配置选项，该选项使系统管理员能够控制是否可以在系统上执行 **xp_cmdshell** 扩展存储过程。 默认情况下， **xp_cmdshell** 选项在新安装的软件上处于禁用状态，但是可以通过使用基于策略的管理或运行 **sp_configure** 系统存储过程来启用它，如下面的代码示例所示：  
  
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
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
