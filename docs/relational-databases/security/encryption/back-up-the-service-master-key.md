---
title: "备份服务主密钥 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- service master key [SQL Server], exporting
ms.assetid: f60b917c-6408-48be-b911-f93b05796904
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 630f9c3ecdf47e6cb7a5d9f2a7970bea99d330a9
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="back-up-the-service-master-key"></a>备份服务主密钥
  本主题介绍如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中备份服务主密钥。 服务主密钥是加密层次结构的根。 应当对服务主密钥进行备份，并将其存储在另外一个安全的位置。 创建该备份应该是首先在服务器上执行的管理操作之一。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   [备份服务主密钥](#Procedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   主密钥必须为打开状态，因此在备份主密钥之前应对其进行解密。 如果使用服务主密钥进行加密，则无需显式打开主密钥；不过，如果只使用密码对主密钥进行加密，则必须显式打开它。  
  
-   我们建议您在创建主密钥之后立即对其进行备份，并存储于另外一个安全的位置中。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 要求对数据库具有 CONTROL 权限。  
  
##  <a name="Procedure"></a> 使用 Transact-SQL  
  
#### <a name="to-back-up-the-service-master-key"></a>备份服务主密钥  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中，连接到包含需要备份的服务主密钥的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例。  
  
2.  选择要用于在备份介质上加密服务主密钥的密码。 此密码应通过复杂性检查。 有关详细信息，请参阅 [Password Policy](../../../relational-databases/security/password-policy.md)。  
  
3.  获得一个用于存储密钥备份副本的可移动备份介质。  
  
4.  确定将在其下创建密钥备份的 NTFS 目录。 这就是在下一步中指定的要创建文件的位置。 应使用高限制级访问控制列表 (ACL) 来保护目录。  
  
5.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
6.  在标准菜单栏上，单击 **“新建查询”**。  
  
7.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- Creates a backup of the "AdventureWorks2012" master key.  
    -- Because this master key is not encrypted by the service master key, a password must be specified when it is opened.  
    USE AdventureWorks2012;  
    GO  
    BACKUP SERVICE MASTER KEY TO FILE = 'c:\temp_backups\keys\service_master_ key'   
        ENCRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
    GO  
    ```  
  
    > [!NOTE]  
    >  指向密钥和密钥的密码（如果有）的文件路径不同于以上所指示的路径。 确保这两个路径都是针对您的服务器和密钥设置的。  
  
8.  将文件复制到备份介质上并验证该副本是否完好。  
  
9. 将备份存储在另外一个安全的位置。  
  
 有关详细信息，请参阅 [OPEN MASTER KEY (Transact-SQL)](../../../t-sql/statements/open-master-key-transact-sql.md) 和 [BACKUP MASTER KEY (Transact-SQL)](../../../t-sql/statements/backup-master-key-transact-sql.md)。  
  
  
