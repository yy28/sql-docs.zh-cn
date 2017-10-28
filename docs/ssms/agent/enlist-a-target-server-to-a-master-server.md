---
title: "将目标服务器登记到主服务器 | Microsoft Docs"
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
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 61fb82bcd0f3ac4308e023e31338f8142614488d
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="enlist-a-target-server-to-a-master-server"></a>将目标服务器登记到主服务器
本主题介绍了如何将目标服务器添加到多服务器管理配置中。 从主服务器运行此过程。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)]，或使用 SQL Server 管理对象 (SMO)。  
  
有关用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服务的 Windows 帐户如何影响多服务器环境的信息，请参阅 [创建多服务器环境](../../ssms/agent/create-a-multiserver-environment.md)。  
  
默认情况下，将为主服务器和目标服务器之间的连接启用完全安全套接字层 (SSL) 加密和证书验证。 有关详细信息，请参阅 [在目标服务器上设置加密选项](../../ssms/agent/set-encryption-options-on-target-servers.md)  
  
**本主题内容**  
  
-   **若要登记目标服务器，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>登记目标服务器  
  
1.  在对象资源管理器中，展开配置为主服务器的服务器。   
  
2.  右键单击“SQL Server 代理”，指向“多服务器管理”，然后单击“添加目标服务器”。  
  
3.  完成目标服务器向导，它将指导您完成该进程。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>登记目标服务器  
  
1.  使用 **sp_msx_enlist** 存储过程。  有关详细信息，请参阅 [sp_msx_enlist (Transact-SQL)](http://msdn.microsoft.com/en-us/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)  
  
## <a name="see-also"></a>另请参阅  
[企业范围的自动化管理](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  

