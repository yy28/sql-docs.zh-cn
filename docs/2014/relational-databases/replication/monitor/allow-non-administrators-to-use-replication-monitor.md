---
title: 允许非管理员使用复制监视器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e0c880bbb7c21ec7d0a766f8bdf0876d4962d10b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219847"
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>允许非管理员使用复制监视器
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中允许非管理员使用复制监视器。 属于下列角色成员的用户可以使用复制监视器：  
  
-   **sysadmin** 固定服务器角色。  
  
     这些用户可以监视复制，并对更改复制属性（如代理计划、代理配置文件等）拥有完全控制权。  
  
-   `replmonitor`分发数据库中的数据库角色。  
  
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
 若要允许非管理员使用复制监视器，隶属**sysadmin**固定的服务器角色必须将用户添加到分发数据库并向该用户分配`replmonitor`角色。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>允许非管理员使用复制监视器  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中，连接到分发服务器，然后展开服务器节点。  
  
2.  依次展开 **“数据库”**、 **“系统数据库”** 和分发数据库（默认名称为 **distribution** ）。  
  
3.  展开 **“安全性”**，右键单击 **“用户”**，然后单击 **“新建用户”**。  
  
4.  输入用户名和用户的登录名。  
  
5.  选择的默认架构`replmonitor`。  
  
6.  选择`replmonitor`中的复选框**数据库角色成员身份**网格。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>将用户添加到 replmonitor 固定数据库角色  
  
1.  在分发服务器上，对分发数据库执行 [sp_helpuser &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpuser-transact-sql)。 如果用户未列在`UserName`中的结果集，用户必须被授予对分发数据库使用的访问[CREATE USER &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-user-transact-sql)语句。  
  
2.  在分发数据库上分发服务器上，执行[sp_helprolemember &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql)，将值指定为`replmonitor`有关**@rolename**参数。 如果列出此用户`MemberName`在结果集中，用户已属于此角色。  
  
3.  如果用户不属于`replmonitor`角色，执行[sp_addrolemember &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)分发服务器上分发数据库。 指定的值`replmonitor`有关**@rolename**和数据库用户的名称或[!INCLUDE[msCoName](../../../includes/msconame-md.md)]所添加的 Windows 登录名**@membername**。  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>从 replmonitor 固定数据库角色中删除用户  
  
1.  若要验证是否为该用户所属`replmonitor`角色，执行[sp_helprolemember &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql)分发服务器上，对分发数据库和指定的值`replmonitor`为**@rolename**. 如果在结果集中的 `MemberName` 中未列出此用户，则此用户当前不属于此角色。  
  
2.  如果用户属于`replmonitor`角色，执行[sp_droprolemember &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)分发服务器上分发数据库。 指定的值`replmonitor`有关**@rolename**和数据库用户或为要删除的 Windows 登录名的名称**@membername**。  
  
  
