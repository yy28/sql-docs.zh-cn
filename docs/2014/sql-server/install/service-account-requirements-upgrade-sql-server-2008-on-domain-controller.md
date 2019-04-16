---
title: 服务升级到 SQL Server 2008 域控制器上的帐户要求 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
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
ms.openlocfilehash: dc00c4195b54101c24bc05218e4ea7c3abac53e8
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582670"
---
# <a name="service-account-requirements-for-upgrading-to-sql-server-2008-on-a-domain-controller"></a>在域控制器上升级到 SQL Server 2008 的服务帐户要求
  升级顾问检测到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上的 Network Service 或 Local Service 帐户下运行[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]域控制器。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装在 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 域控制器上，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务不能以 Local Service 帐户或 Network Service 帐户特权运行。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 请确保对所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户都分配了 Domain 帐户或 Local System 帐户。 如果不能在升级之前完成此更改，将阻止安装程序运行。 SQL Writer、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Active Directory Helper 服务的服务帐户例外，因为它们已硬编码到 Network Service 帐户，无法进行更改。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
