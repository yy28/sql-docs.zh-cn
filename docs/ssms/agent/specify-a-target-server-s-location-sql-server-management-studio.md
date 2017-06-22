---
title: "指定目标服务器位置 | Microsoft Docs"
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
- SQL Server Agent jobs, target servers
- target servers [SQL Server], location
ms.assetid: 511ff311-21f5-4f2f-839f-b4deee26ec98
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e287e48b3185904eb2fb5b24920aa3dca433fcff
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="specify-a-target-server39s-location-sql-server-management-studio"></a>指定目标服务器的位置 (SQL Server Management Studio)
本主题介绍了如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 在 [!INCLUDE[tsql](../../includes/tsql_md.md)]的多服务器管理配置中指定目标服务器的位置。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [限制和局限](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要指定目标服务器的位置，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
执行此操作将编辑注册表。 建议不要手动编辑注册表，因为不适当或不正确的更改会导致严重的系统配置问题。 因此，只有有经验的用户才可以使用注册表编辑器程序编辑注册表。 有关详细信息，请参阅 Microsoft Windows 文档。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-specify-a-target-servers-location"></a>指定目标服务器的位置  
  
1.  在 **“对象资源管理器”**中，单击加号以展开要指定目标服务器的位置的 master 服务器。  
  
2.  右键单击“SQL Server 代理”，指向“多服务器管理”，然后选择“管理目标服务器”。  
  
3.  右键单击某一目标服务器，再选择“属性”。  
  
4.  在 **“位置”** 框中，输入该服务器的位置，然后单击 **“确定”**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-specify-a-target-servers-location"></a>指定目标服务器的位置  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    USE msdb ;  
    GO  
    -- enlists the current server into the AdventureWorks1 master server.   
    -- The location for the current server is Building 21, Room 309, Rack 5  
    EXEC dbo.sp_msx_enlist N'AdventureWorks2012',   
        N'Building 21, Room 309, Rack 5' ;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_msx_enlist (Transact-SQL)](http://msdn.microsoft.com/en-us/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)。  
  

