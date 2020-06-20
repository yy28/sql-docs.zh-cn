---
title: 重命名与固定服务器角色名称匹配的登录名 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- user-defined login names [SQL Server]
- fixed server roles [SQL Server]
- renamed logins [SQL Server]
- logins [SQL Server], names
ms.assetid: 10a1d77c-3153-474f-a6a0-969556794467
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 296ae4d4051e79e3c5d3bc158ef3e87c9164ecd3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059087"
---
# <a name="rename-logins-matching-fixed-server-role-names"></a>重命名与固定服务器角色名称匹配的登录名
  升级顾问检测到有一个或多个用户定义的登录名与固定服务器角色的名称匹配。 固定服务器角色名称是保留名称。 请在升级前重命名相应登录名。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
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
  
3.  使用**sp_addlogin**系统过程创建新登录名。 为每个相应的登录名指定** \@ sid**参数的步骤1中返回的 sid。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
