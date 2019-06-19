---
title: SQL Server 登录密码强度 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b0862c3a-926b-490c-a37f-382e50146a3e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1b2c130ace15d6bd4afec307824099c649214e0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253294"
---
# <a name="sql-server-login-password-strength"></a>SQL Server 登录密码强度
  此规则检查是否每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名都已启用“强制实施密码策略”。 如果启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证并且操作系统版本低于 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]，则攻击者可能会重复利用已知的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录密码。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 建议将操作系统升级到 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]。  
  
 如果您的环境中不需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请使用 Windows 身份验证。  
  
 为所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名启用“强制实施密码策略”。 使用 [ALTER LOGIN](/sql/t-sql/statements/alter-login-transact-sql) 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名配置密码策略。  
  
## <a name="for-more-information"></a>有关详细信息  
 [密码策略](../security/password-policy.md)  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
