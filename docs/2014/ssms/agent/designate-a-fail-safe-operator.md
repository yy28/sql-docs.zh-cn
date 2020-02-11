---
title: 指定防故障操作员 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- fail-safe operator [SQL Server]
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 0f4eb513-5c0a-4523-974e-e85c1deeb57f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54ec71df8efab1f60bfb7a5b9af448705e349d28
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211427"
---
# <a name="designate-a-fail-safe-operator"></a>指定防故障操作员
  防故障操作员是在无法联系到指定的操作员时接收警报的用户。 本主题说明如何通过使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]在中设置防故障操作员以接收代理警报通知。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要指定防故障操作员，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   在未来版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，将从代理中删除寻呼程序和**net send**选项。 请避免在新的开发工作中使用这些功能，并考虑修改当前使用这些功能的应用程序。  
  
-   请注意，若要向操作员发送电子邮件和寻呼通知，必须将 SQL Server 代理配置为使用数据库邮件。 有关详细信息，请参阅 [向操作员分配警报](assign-alerts-to-an-operator.md)。  
  
-   
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 为管理作业提供了一种图形化的简便方法，建议使用此方法来创建和管理作业基础结构。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 权限  
 只有 **sysadmin** 固定服务器角色的成员才能指定防故障操作员。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-designate-a-fail-safe-operator"></a>指定防故障操作员  
  
1.  在“对象资源管理器”**** 中，单击加号以展开服务器，该服务器包含要指定为防故障操作员的 SQL Server 代理操作员。  
  
2.  右键单击“SQL Server 代理”****，然后选择“属性”****。  

3.  在 " **SQL Server 代理属性-**_server_name_ " 对话框中的 "**选择页**" 下，选择 "**警报系统**"。  
 
4.  在“防故障操作员”**** 下，选中“启用防故障操作员”****。  
  
5.  在“操作员”**** 列表中，选择想要执行防故障的操作员。  
  
6.  选中以下任何或所有复选框以指定通知操作员的方法：“电子邮件”****、“寻呼程序”**** 或“Net send”****。  
  
7.  完成后，单击 **“确定”** 。  
  
  
