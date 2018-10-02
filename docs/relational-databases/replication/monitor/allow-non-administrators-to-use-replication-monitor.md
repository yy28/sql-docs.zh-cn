---
title: 允许非管理员使用复制监视器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e163616fc8cf99ea2a70dfab01d2a420bec1d9f5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717975"
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>允许非管理员使用复制监视器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中允许非管理员使用复制监视器。 属于下列角色成员的用户可以使用复制监视器：  
  
-   **sysadmin** 固定服务器角色。  
  
     这些用户可以监视复制，并对更改复制属性（如代理计划、代理配置文件等）拥有完全控制权。  
  
-   分发数据库中的 **replmonitor** 数据库角色。  
  
     这些用户可以监视复制，但不能更改任何复制属性。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **允许非管理员使用复制监视器，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 若要允许非管理员使用复制监视器， **sysadmin** 固定服务器角色的成员必须将用户添加到分发数据库，并向该用户分配 **replmonitor** 角色。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>允许非管理员使用复制监视器  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中，连接到分发服务器，然后展开服务器节点。  
  
2.  依次展开 **“数据库”**、 **“系统数据库”** 和分发数据库（默认名称为 **distribution** ）。  
  
3.  展开 **“安全性”**，右键单击 **“用户”**，然后单击 **“新建用户”**。  
  
4.  输入用户名和用户的登录名。  
  
5.  选择默认的 **replmonitor**架构。  
  
6.  在 **“数据库角色成员身份”** 网格中，选中 **“replmonitor”** 复选框。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>将用户添加到 replmonitor 固定数据库角色  
  
1.  在分发服务器上，对分发数据库执行 [sp_helpuser &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)。 如果未在结果集中的 **UserName** 中列出此用户，则必须使用 [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md) 语句为用户授予对分发数据库的访问权限。  
  
2.  在分发数据库上的分发服务器中，执行 [sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)，并为 **@rolename** 参数指定 **replmonitor** 值。 如果在结果集中的 **MemberName** 中列出此用户，则此用户已属于此角色。  
  
3.  如果此用户不属于 **replmonitor** 角色，则在分发服务器的分发数据库中执行 [sp_addrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)。 为 **replmonitor** @rolename **@rolename** 并为 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] @membername **@membername**中允许非管理员使用复制监视器。  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>从 replmonitor 固定数据库角色中删除用户  
  
1.  若要验证用户是否属于 **replmonitor** 角色，请在分发数据库上的分发服务器中执行 [sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)，并为 **@rolename** 指定 **replmonitor** 值。 如果在结果集中的 **MemberName** 中未列出此用户，则此用户当前不属于此角色。  
  
2.  如果此用户属于 **replmonitor** 角色，则在分发服务器的分发数据库中执行 [sp_droprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)。 为 **replmonitor** @rolename **@rolename** 并为 **@membername**中允许非管理员使用复制监视器。  
  
  
