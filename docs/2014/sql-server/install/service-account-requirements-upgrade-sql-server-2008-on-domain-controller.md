---
title: 升级到域控制器上的 SQL Server 2008 的服务帐户要求 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- domain controllers
- service accounts
- network service accounts
- local service accounts
ms.assetid: 574245b6-11e2-4849-b0ca-836d673ecd0d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bb703e42edcbf128ff78ca294e08fc487f06d8f8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092257"
---
# <a name="service-account-requirements-for-upgrading-to-sql-server-2008-on-a-domain-controller"></a>在域控制器上升级到 SQL Server 2008 的服务帐户要求
  升级顾问检测到在网络[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务或[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]域控制器上的本地服务帐户下运行的实例。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装在 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 域控制器上，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务不能以 Local Service 帐户或 Network Service 帐户特权运行。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 请确保对所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户都分配了 Domain 帐户或 Local System 帐户。 如果不能在升级之前完成此更改，将阻止安装程序运行。 SQL Writer、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Active Directory Helper 服务的服务帐户例外，因为它们已硬编码到 Network Service 帐户，无法进行更改。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
