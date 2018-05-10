---
title: SQL Server 登录密码过期 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 7e3bf9da-a436-433d-847a-47c30428cad3
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 81140c252be05bb75bee1800a988fe70e67d2bf0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-login-password-expiration"></a>SQL Server 登录密码过期
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此规则检查是否每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名都已启用“密码过期”。 如果启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证并且操作系统版本低于 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]，则攻击者可能会重复利用已知的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录密码。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 建议将操作系统升级到 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]。  
  
 如果您的环境中不需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请使用 Windows 身份验证。 有关详细信息，请参阅 [选择身份验证模式](../../relational-databases/security/choose-an-authentication-mode.md)。  
  
 为所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名启用“密码过期”。 使用 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名配置密码策略。  
  
## <a name="for-more-information"></a>有关详细信息  
 [密码策略](../../relational-databases/security/password-policy.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
