---
title: "立即应用成员权限 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- members [Master Data Services], applying permissions immediately
- permissions [Master Data Services], applying member permissions immediately
ms.assetid: 5b16de66-5c39-49f5-992f-402a9eb319aa
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: a3ac0d4510b77c5e0c6fe95ff7cbf2c6aae433be
ms.contentlocale: zh-cn
ms.lasthandoff: 09/07/2017

---
# <a name="immediately-apply-member-permissions-master-data-services"></a>立即应用成员权限 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以立即应用成员权限，而不必等待定期应用的成员安全性。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须具有在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中执行 mdm.udpSecurityMemberProcessRebuildModel 存储过程的权限。 有关详细信息，请参阅[数据库对象安全性 (Master Data Services)](../master-data-services/database-object-security-master-data-services.md)。  
  
### <a name="to-immediately-apply-hierarchy-member-permissions"></a>立即应用层次结构成员权限  
  
1.  打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 并连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 数据库的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 实例。  
  
2.  创建新查询。  
  
3.  键入以下文本，用数据库名称替换 database，用模型名称替换 Model_Name。  
  
    ```  
    USE [database];  
    GO  
  
    DECLARE @Model_ID INT;  
    SELECT @Model_ID = ID FROM mdm.tblModel WHERE [Name] = N'Model_Name';  
    EXEC [mdm].[udpSecurityMemberProcessRebuildModel] @Model_ID=@Model_ID, @ProcessNow=1;  
    GO  
    ```  
  
4.  运行查询。  
  
## <a name="see-also"></a>另请参阅  
 [分配层次结构成员权限 (Master Data Services)](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [层次结构成员权限 (Master Data Services)](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  

