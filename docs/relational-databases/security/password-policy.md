---
title: "密码策略 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "09/25/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ALTER LOGIN 语句"
  - "密码 [SQL Server], 策略实施"
  - "登录名 [SQL Server], 密码"
  - "CHECK_EXPIRATION 选项"
  - "复杂密码 [SQL Server]"
  - "密码 [SQL Server], 过期"
  - "重置手动错误密码计数"
  - "MUST_CHANGE 选项"
  - "过期 [SQL Server]"
  - "过期密码 [SQL Server]"
  - "符号 [SQL Server]"
  - "NetValidatePasswordPolicy() API"
  - "密码 [SQL Server]"
  - "密码策略 [SQL Server]"
  - "重置错误密码计数"
  - "安全性 [SQL Server], 密码"
  - "CHECK_POLICY 选项"
  - "密码 [SQL Server], 符号"
  - "错误的密码计数"
  - "密码 [SQL Server], 复杂性"
  - "字符 [SQL Server], 密码策略"
ms.assetid: c0040c0a-a18f-45b9-9c40-0625685649b1
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# 密码策略
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以使用 Windows 密码策略机制。 密码策略应用于使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的登录名，并且应用于具有密码的包含数据库用户。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以对在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内部使用的密码应用在 Windows 中使用的相同复杂性策略和过期策略。 此功能取决于 `NetValidatePasswordPolicy` API。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 强制实施密码复杂性。 密码过期和策略实施部分不适用于 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
## 密码复杂性  
 密码复杂性策略通过增加可能密码的数量来阻止强力攻击。 实施密码复杂性策略时，新密码必须符合以下原则：  
  
-   密码不得包含用户的帐户名。  
  
-   密码长度至少为八个字符。  
  
-   密码包含以下四类字符中的三类：  
  
    -   拉丁文大写字母 (A - Z)  
  
    -   拉丁文小写字母 (a - z)  
  
    -   10 个基本数字 (0 - 9)  
  
    -   非字母数字字符，如感叹号 (!)、美元符号 ($)、数字符号 (#) 或百分号 (%)。  
  
 密码可最长为 128 个字符。 使用的密码应尽可能长，尽可能复杂。  
  
## 密码过期  
 密码过期策略用于管理密码的使用期限。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实施密码过期策略，则系统将提醒用户更改旧密码，并禁用带有过期密码的帐户。  
  
## 策略实施  
 可为每个 SQL Server 登录名单独配置密码策略实施。 使用 [ALTER LOGIN (Transact-SQL)](../../t-sql/statements/alter-login-transact-sql.md) 来配置 SQL Server 登录名的密码策略选项。 配置密码策略实施时，适用以下规则：  
  
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
  
## 相关任务  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)  
  
 [CREATE USER (Transact-SQL)](../../t-sql/statements/create-user-transact-sql.md)  
  
 [ALTER USER (Transact-SQL)](../../t-sql/statements/alter-user-transact-sql.md)  
  
 [创建一个登录名](../../relational-databases/security/authentication-access/create-a-login.md)  
  
 [创建数据库用户](../../relational-databases/security/authentication-access/create-a-database-user.md)  
  
## 相关内容  
 [强密码](../../relational-databases/security/strong-passwords.md)  
  
  