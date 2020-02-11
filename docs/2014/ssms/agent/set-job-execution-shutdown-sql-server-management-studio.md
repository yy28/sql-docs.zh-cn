---
title: 设置作业执行关闭 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
- SQL Server Agent jobs, execution shutdowns
ms.assetid: ac23e88f-53fc-41de-bb16-0c27c002d5a5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca9343fe8a6f9e89ba9f26dbbbb12dd7362aff91
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63033596"
---
# <a name="set-job-execution-shutdown-sql-server-management-studio"></a>Set Job Execution Shutdown (SQL Server Management Studio)
  本主题介绍如何设置[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理在通过使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]在中完成前等待执行作业的时间。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要为 SQL Server 代理作业设置关闭时间，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 权限  
 默认情况下， **sysadmin** 固定服务器角色的成员可设置在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理等待作业执行完的时间。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-job-execution-shutdown"></a>设置作业执行关闭  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要设置作业执行关闭间隔的服务器。  
  
2.  右键单击“SQL Server 代理”****，然后选择“属性”****。  
  
3.  在 **“选择页”** 下，选择 **“作业系统”**。  
  
4.  设置“关闭超时间隔(秒)”**** 以延长或缩短关闭超时间隔。 这决定了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理本身结束之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理等待作业执行完成的时间长度。  
  
  
