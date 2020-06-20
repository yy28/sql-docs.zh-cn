---
title: 使用新的存储过程替换 xp_sqlagent_proxy_account 扩展存储过程的使用情况 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- xp_sqlagent_proxy_account
ms.assetid: 0e3cc931-6237-41dd-bf0d-0c03f4d8fff2
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 46de12faa52fae61e1f11758f40e1ec8242faca1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011859"
---
# <a name="replace-usage-of-the-xp_sqlagent_proxy_account-extended-stored-procedure-with-new-stored-procedures"></a>用新存储过程代替使用的 xp_sqlagent_proxy_account 扩展存储过程
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理支持多个代理帐户。 您可使用一组新的存储过程来定义这些代理帐户。 有关新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理存储过程的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的以下主题：  
  
-   "sp_add_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_delete_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_enum_login_for_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_enum_proxy_for_subsystem ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_enum_sqlagent_subsystems ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_grant_proxy_to_subsystem ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_grant_login_to_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_help_proxy" ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_revoke_login_from_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_revoke_proxy_from_subsystem ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_update_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
> [!NOTE]  
>  升级到之后 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ，使用**xp_sqlagent_proxy_account**扩展存储过程的任何语句都将不起作用。 使用**sp_xp_cmdshell_proxy_account**而不是**xp_sqlagent_proxy_account**来设置**xp_cmdshell**的代理。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 代理升级问题](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
