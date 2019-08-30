---
title: 第 4 课：从完整数据库备份执行还原 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 580f76e6-9802-4abc-9043-db6de592c733
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: de9a356589ac6bceb532ed4cecf509f957e3c337
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153399"
---
# <a name="lesson-4-perform-a-restore-from-a-full-database-backup"></a>第 4 课：从完整数据库备份执行还原
  本课演示如何使用 tsql 语句从上一课所创建的完整数据库备份中执行还原。  
  
## <a name="perform-a-restore-of-a-database-backup"></a>执行数据库备份的还原  
 若要还原完整数据库备份，请使用以下步骤：  
  
1.  连接到 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
2.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]的实例。  
  
3.  在标准菜单栏上，单击 **“新建查询”** 。  
  
4.  将以下示例复制并粘贴到查询窗口中，并根据需要进行修改。  
  
    ```  
    RESTORE DATABASE AdventureWorks2012   
    FROM URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    WITH CREDENTIAL = 'mycredential';  
    , STATS = 5 - use this to see monitor the progress  
    GO  
  
    ```  
  
5.  验证 T-sql 语句, 然后单击 "**执行**"  
  
### <a name="return-to-tutorials-portal"></a>返回到教程入门  
 [教程：SQL Server 备份和还原到 Azure Blob 存储服务](../relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)。  
  
  
