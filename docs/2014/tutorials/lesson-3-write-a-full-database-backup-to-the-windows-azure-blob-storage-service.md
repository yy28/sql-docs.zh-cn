---
title: 第 3 课： 将完整数据库备份写入到 Windows Azure Blob 存储服务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 454c8296-64e9-46ed-b141-5ebfbc8a4fe2
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: f0de77c43dc2a18bbbb4496f6c1d1c3aab21de96
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172267"
---
# <a name="lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service"></a>第 3 课：将完整数据库备份写入到 Windows Azure Blob 存储服务
  本课演示如何使用 tsql 语句执行到 Windows Azure Blob 存储服务的完整数据库备份。  
  
## <a name="perform-a-full-database-backup-to-the-windows-azure-blob-storage-service"></a>执行到 Windows Azure Blob 存储服务的完整数据库备份  
 若要创建完整数据库备份，请使用以下步骤：  
  
1.  连接到 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
2.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]的实例。  
  
3.  在标准菜单栏上，单击 **“新建查询”**。  
  
4.  将以下示例复制并粘贴到查询窗口中，根据需要进行修改，然后单击 **“执行”**。  
  
    ```  
    BACKUP DATABASE[AdventureWorks2012]   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    /* URL includes the endpoint for the BLOB service, followed by the container name, and the name of the backup file*/   
    WITH CREDENTIAL = 'mycredential';  
    /* name of the credential you created in the previous step */   
    GO  
  
    ```  
  
5.  在对象资源管理器中，连接到 Azure 存储。 通过浏览找到容器和新创建的备份文件。  
  
## <a name="next-lesson"></a>下一课  
 [第 4 课： 从完整数据库备份执行还原](../../2014/tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)。  
  
  
