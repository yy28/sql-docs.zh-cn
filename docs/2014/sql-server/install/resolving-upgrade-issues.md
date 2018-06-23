---
title: 解决升级问题 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing Upgrade Advisor
- Upgrade Advisor [SQL Server], reference
- component issue resolution [Upgrade Advisor]
- resolving upgrade issues
- upgrade blocks [Upgrade Advisor]
- detecting upgrade issues
- finding upgrade issues
- Upgrade Advisor [SQL Server], blocking issues
- configurations preventing upgrading [Upgrade Advisor]
- locating upgrade issues
- blocking issues [Upgrade Advisor]
- issues preventing upgrading [Upgrade Advisor]
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, reference
- analyzing system [Upgrade Advisor], resolving issues
- settings preventing upgrading [Upgrade Advisor]
- upgrade issue reference [Upgrade Advisor]
- identifying upgrade issues
- fixing upgrade issues [Upgrade Advisor]
ms.assetid: 113eb435-8d36-4ed6-9790-b5e4c14809c8
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6072fb3c1d52048832bd6d07f34828c84eb2d491
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027135"
---
# <a name="resolving-upgrade-issues"></a>解决升级问题
  本节主题介绍可以检测到的升级问题以及虽然检测不到但可能会对升级和升级后的使用造成影响的问题。 这些问题按 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件编排。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [最新升级问题](../../../2014/sql-server/install/late-breaking-upgrade-issues.md)  
  
-   [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
-   [全文搜索升级问题](../../../2014/sql-server/install/full-text-search-upgrade-issues.md)  
  
-   [复制升级问题](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
-   [Reporting Services 升级问题&#40;升级顾问&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
-   [SQL Server 代理升级问题](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
## <a name="issues-that-prevent-upgrading"></a>阻止升级的问题  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的之前版本中的一些配置或设置可阻止您升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 如果在您安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 时安装程序检测到这些问题，则安装程序停止升级过程，并请求您运行升级顾问和修复阻碍升级的所有问题。  
  
### [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 升级报表中列出了以下任务，则在升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之前必须执行相应的所需操作：  
  
-   [分离数据库 ID 32767](../../../2014/sql-server/install/detach-database-id-32767.md)  
  
-   [重命名登录名与固定的服务器角色名称匹配](../../../2014/sql-server/install/rename-logins-matching-fixed-server-role-names.md)  
  
-   [重命名用户 sys](../../../2014/sql-server/install/rename-user-sys.md)  
  
-   [使用 sp_rename 重命名重复的索引名称](../../../2014/sql-server/install/use-sp-rename-to-rename-duplicate-index-name.md)  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
