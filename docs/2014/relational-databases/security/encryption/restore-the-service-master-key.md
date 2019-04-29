---
title: 还原服务主密钥 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server], importing
- service master key [SQL Server], restoring
ms.assetid: 14bdbbbe-d384-4692-b670-4243d2466fe1
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 17a404ef96b4800aa072b8f35c2d22c349361ca3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011552"
---
# <a name="restore-the-service-master-key"></a>还原服务主密钥
  本主题介绍如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中还原服务主密钥。  
  
> [!WARNING]  
>  您可能永远也不需要还原服务主密钥。 但如果进行此操作，应当格外谨慎。 有关详细信息，请参阅 [Back Up the Service Master Key](service-master-key.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   [使用 Transact-SQL 还原服务主密钥](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   当还原服务主密钥时， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将对所有已使用当前服务主密钥加密的密钥和机密内容进行解密，然后使用从备份文件中加载的服务主密钥对这些密钥和机密内容进行加密。  
  
-   如果有任意一种解密操作失败，则还原操作将会失败。 您可以使用 FORCE 选项忽略错误，但是该选项会使无法进行解密的数据丢失。  
  
-   重新生成加密层次结构是一种消耗大量资源的操作。 您应当将该操作安排在资源需求较低的时段进行。  
  
> [!CAUTION]  
>  服务主密钥为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密层次结构的根。 服务主密钥直接或间接地保护树中的所有其他密钥。 如果在强制的还原过程中不能对某个相关密钥进行解密，则由该密钥所保护的数据便会丢失。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要对服务器的 CONTROL SERVER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-restore-the-service-master-key"></a>还原服务主密钥  
  
1.  从物理备份介质或本地文件系统上的某个目录检索备份的服务主密钥的副本。  
  
2.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
3.  在标准菜单栏上，单击 **“新建查询”**。  
  
4.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- Restores the service master key from a backup file.  
    RESTORE SERVICE MASTER KEY   
        FROM FILE = 'c:\temp_backups\keys\service_master_key'   
        DECRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
    GO  
    ```  
  
    > [!NOTE]  
    >  指向密钥和密钥的密码（如果有）的文件路径不同于以上所指示的路径。 请确保这两个路径都是针对您的服务器和密钥设置的。  
  
  
