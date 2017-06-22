---
title: "指定事件转发服务器 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3a888bf925f0deec6b774891d13da7548d1fe28f
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="designate-an-events-forwarding-server-sql-server-management-studio"></a>Designate an Events Forwarding Server (SQL Server Management Studio)
本主题介绍了如何通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中为 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 指定接收转发事件的服务器。 请注意，事件转发适用于在服务器之间转发的事件，而不适用于在单个计算机上承载的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 实例之间转发的事件。 此外，还请注意，为了接收转发的事件，警报管理服务器必须是 SQL Server 的默认实例。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [Security](#Security)  
  
-   **若要指定事件转发服务器，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-designate-an-events-forwarding-server"></a>指定事件转发服务器  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要将其事件转发到其他服务器的服务器。  
  
2.  右键单击“SQL Server 代理”，然后选择“属性”。  
  
3.  在“SQL Server 代理属性 – server_name”对话框中，在“选择页面”下，选择“高级”。  
  
4.  在 **“SQL Server 事件转发”**下，选中 **“将事件转发到其他服务器”** 复选框。  
  
5.  在 **“服务器”** 列表中，选择一台服务器，然后在 **“事件”**选择下列操作之一：  
  
    -   选择 **“未处理的事件”** 以仅转发本地警报未处理的事件。  
  
    -   选择 **“所有事件”** 以转发所有事件，无论本地警报是否已对事件进行处理。  
  
6.  在 **“如果事件的严重性不低于”** 列表中，单击将事件转发到所选服务器时的严重级别。  
  
7.  完成后，单击 **“确定”**。  
  

