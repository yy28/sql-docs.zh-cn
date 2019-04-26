---
title: 无法升级休眠的 SQL Server 6.5 登录名 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- passwords [SQL Server], dormant logins
- dormant logins
- logins [SQL Server], upgrading dormant logins
- identifying dormant logins
- password hashes [SQL Server]
ms.assetid: ebe18a74-0375-4df4-b894-239f8fdabb64
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0381e04ae1df53e5502c49eb17d0823fcf611e89
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62645823"
---
# <a name="dormant-sql-server-65-logins-cannot-be-upgraded"></a>无法升级休眠的 SQL Server 6.5 登录名
  升级顾问检测到了其密码不能直接升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 登录名。  
  
 若要启用此登录名，必须重置其密码。 使用 ALTER LOGIN 可以重置密码。  
  
```  
ALTER LOGIN <login name> WITH PASSWORD = '<new password>' MUST_CHANGE  
```  
  
 除非禁用了策略检查，否则将根据系统的密码复杂性策略来验证新密码。 建议使用复杂的密码且不要禁用策略检查。 MUST_CHANGE 选项将强制用户选择新密码。 这不是必需的，但建议这样做。  
  
 通过使用以下查询可以标识休眠的登录名：  
  
```  
SELECT * FROM sysxlogins WHERE (xstatus & 2048) = 2048;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
