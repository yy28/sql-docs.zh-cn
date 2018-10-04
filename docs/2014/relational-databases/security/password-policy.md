---
title: 密码策略 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- ALTER LOGIN statement
- passwords [SQL Server], policy enforcement
- logins [SQL Server], passwords
- CHECK_EXPIRATION option
- complex passwords [SQL Server]
- passwords [SQL Server], expiration
- manual bad password count resets
- MUST_CHANGE option
- expiration [SQL Server]
- expired password [SQL Server]
- symbols [SQL Server]
- NetValidatePasswordPolicy() API
- passwords [SQL Server]
- password policy [SQL Server]
- resetting bad password counts
- security [SQL Server], passwords
- CHECK_POLICY option
- passwords [SQL Server], symbols
- bad password counts
- passwords [SQL Server], complexity
- characters [SQL Server], password policies
ms.assetid: c0040c0a-a18f-45b9-9c40-0625685649b1
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7b28043d797585496686dea6fd0c5fad276f16b9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049977"
---
# <a name="password-policy"></a>密码策略
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以使用 Windows 密码策略机制。 密码策略应用于使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的登录名，并且应用于具有密码的包含数据库用户。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以对在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内部使用的密码应用在 Windows 中使用的相同复杂性策略和过期策略。 此功能取决于 `NetValidatePasswordPolicy` API。  
  
## <a name="password-complexity"></a>密码复杂性  
 密码复杂性策略通过增加可能密码的数量来阻止强力攻击。 实施密码复杂性策略时，新密码必须符合以下原则：  
  
-   密码不得包含用户的帐户名。  
  
-   密码长度至少为八个字符。  
  
-   密码包含以下四类字符中的三类：  
  
    -   拉丁文大写字母 (A - Z)  
  
    -   拉丁文小写字母 (a - z)  
  
    -   10 个基本数字 (0 - 9)  
  
    -   非字母数字字符，如感叹号 (!)、美元符号 ($)、数字符号 (#) 或百分号 (%)。  
  
 密码可最长为 128 个字符。 使用的密码应尽可能长，尽可能复杂。  
  
## <a name="password-expiration"></a>密码过期  
 密码过期策略用于管理密码的使用期限。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实施密码过期策略，则系统将提醒用户更改旧密码，并禁用带有过期密码的帐户。  
  
## <a name="policy-enforcement"></a>策略实施  
 可为每个 SQL Server 登录名单独配置密码策略实施。 使用 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql) 来配置 SQL Server 登录名的密码策略选项。 配置密码策略实施时，适用以下规则：  
  
-   如果 CHECK_POLICY 改为 ON，则将出现以下行为：  
  
    -   除非将 CHECK_EXPIRATION 显式设置为 OFF，否则也会将其设置为 ON。  
  
    -   用当前的密码哈希值初始化密码历史记录。  
  
    -   还将启用**帐户锁定时间**, **帐户锁定阈值**和 **在此后重置帐户锁定计数器** 。  
  
-   如果 CHECK_POLICY 改为 OFF，则将出现以下行为：  
  
    -   CHECK_EXPIRATION 也设置为 OFF。  
  
    -   清除密码历史记录。  
  
    -   `lockout_time` 的值被重置。  
  
 不支持策略选项的某些组合。  
  
-   如果指定 MUST_CHANGE，则 CHECK_EXPIRATION 和 CHECK_POLICY 必须设置为 ON。 否则，该语句将失败。  
  
-   如果 CHECK_POLICY 设置为 OFF，则 CHECK_EXPIRATION 不能设置为 ON。 包含此选项组合的 ALTER LOGIN 语句将失败。  
  
 设置 CHECK_POLICY = ON 将禁止创建以下类型的密码：  
  
-   为 NULL 或空  
  
-   与计算机名或登录名相同  
  
-   下列任意项：“password”、“admin”、“administrator”、“sa”、“sysadmin”  
  
 可以在 Windows 中设置安全策略，也可以从域接收安全策略。 若要查看计算机上的密码策略，请使用本地安全策略 MMC 管理单元 (**secpol.msc**)。  
  
## <a name="related-tasks"></a>Related Tasks  
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
 [CREATE USER (Transact-SQL)](/sql/t-sql/statements/create-user-transact-sql)  
  
 [ALTER USER (Transact-SQL)](/sql/t-sql/statements/alter-user-transact-sql)  
  
 [创建一个登录名](authentication-access/create-a-login.md)  
  
 [创建数据库用户](authentication-access/create-a-database-user.md)  
  
## <a name="related-content"></a>相关内容  
 [强密码](strong-passwords.md)  
  
  
