---
title: 重命名与固定的服务器角色名称匹配的登录名 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- user-defined login names [SQL Server]
- fixed server roles [SQL Server]
- renamed logins [SQL Server]
- logins [SQL Server], names
ms.assetid: 10a1d77c-3153-474f-a6a0-969556794467
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fa2e74dfc1afdfe25058657d910315a3fb626f1c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855457"
---
# <a name="rename-logins-matching-fixed-server-role-names"></a>重命名与固定服务器角色名称匹配的登录名
  升级顾问检测到有一个或多个用户定义的登录名与固定服务器角色的名称匹配。 固定服务器角色名称是保留名称。 请在升级前重命名相应登录名。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 以下固定服务器角色名称是保留名称，因此不能用作用户定义的登录名。  
  
-   **sysadmin**  
  
-   **serveradmin**  
  
-   **setupadmin**  
  
-   **securityadmin**  
  
-   **processadmin**  
  
-   **dbcreator**  
  
-   **diskadmin**  
  
-   **bulkadmin**  
  
## <a name="corrective-action"></a>纠正措施  
 在升级之前，请先执行以下步骤：  
  
1.  通过执行以下语句来记录登录名的安全标识符 (SID)。  
  
    ```  
    SELECT name, sid   
    FROM master.dbo.syslogins   
    WHERE name IN('sysadmin', 'serveradmin','setupadmin', 'securityadmin','processadmin', 'dbcreator','diskadmin','bulkadmin')  
    ```  
  
2.  删除登录名。  
  
3.  使用**sp_addlogin**系统过程来创建新的登录名。 指定在步骤 1 中返回的 SID **@sid**参数为每个相应登录名。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
