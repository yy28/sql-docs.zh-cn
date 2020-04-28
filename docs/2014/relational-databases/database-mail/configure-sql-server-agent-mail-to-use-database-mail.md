---
title: 配置 SQL Server 代理邮件以使用数据库邮件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], SQL Server Agent Mail
- SQL Server Agent Mail
ms.assetid: 4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d3c2f5f0be09e9a60997308efd72c360348efc60
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "79289205"
---
# <a name="configure-sql-server-agent-mail-to-use-database-mail"></a>配置 SQL Server 代理邮件以使用数据库邮件
  本主题说明如何配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理以使用数据库邮件通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 发送 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的通知和警报。  
  
-   **开始之前：**  
  
-   [先决条件](#Prerequisites)  
  
-   [安全性](#Security)  
  
-   [使用 SQL Server Management Studio 配置 SQL Server 代理以使用数据库邮件](#SSMSProcedure)  
  
-   [跟进任务](#Follow_Up)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
  
-   启用数据库邮件。  
  
-   创建供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户使用的数据库邮件帐户。  
  
-   创建供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户使用的数据库邮件配置文件，并将用户添加到 **msdb** 数据库的 **DatabaseMailUserRole** 中。  
  
-   将该配置文件设置为 **msdb** 数据库的默认配置文件。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 创建配置文件帐户和执行存储过程的用户应是 sysadmin 固定服务器角色的成员。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **配置 SQL Server 代理邮件以使用数据库邮件**  
  
-   在对象资源管理器中，展开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
-   右键单击“SQL Server 代理”****，然后单击“属性”****。  
  
-   单击 **“警报系统”**。  
  
-   选择 **“启用邮件配置文件”**。  
  
-   在 **“邮件系统”** 列表中，选择 **“数据库邮件”**。  
  
-   在 **“邮件配置文件列表”** 中，为数据库邮件选择一个邮件配置文件。  
  
-   重新启动 SQL Server 代理。  
  
##  <a name="follow-up-tasks"></a><a name="Follow_Up"></a> 后续任务  
 需要执行下列任务以完成对发送警报和通知的代理配置。  
  
-   [警报](../../ssms/agent/alerts.md)  
  
     可以配置警报，将特定数据库事件或操作系统情况通知操作员。  
  
-   [运算符](../../ssms/agent/operators.md)  
  
     操作员是可以接收电子通知的人员或组的别名  
  
  
