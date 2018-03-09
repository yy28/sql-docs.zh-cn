---
title: "第 3 课：将数据库备份到 URL | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 804f853ada6e3fe3cdbfc3964f3201d1a38cce80
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
---
# <a name="lesson-3-database-backup-to-url"></a>第 3 课：将数据库备份到 URL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在本课程中，你会将本地 SQL Server 2016 实例上的 AdventureWorks2014 数据库备份到在 [第 1 课：在 Azure 容器上创建存储访问策略和共享访问签名](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)中创建的 Azure 容器。  
  
> [!NOTE]  
> 如果要将 SQL Server 2012 SP1 CU2 或更高版本数据库或 SQL Server 2014 数据库备份到此 Azure 容器，则可以通过 [此处](https://technet.microsoft.com/en-US/library/dn435916(v=sql.120).aspx) 记录的已弃用语法，使用 WITH CREDENTIAL 语法备份到 URL。  
  
若要将数据库备份到 Blob 存储，请执行以下步骤：  
  
1.  连接到 SQL Server Management Studio。  
  
2.  打开一个新查询窗口，连接到 Azure 虚拟机中数据库引擎的 SQL Server 2016 实例。  
  
3.  复制以下 Transact-SQL 脚本，然后将其粘贴到查询窗口中。 将 URL 中的存储帐户名称和容器名称更改为第 1 课中指定的名称，然后执行此脚本。  
  
    ```  
  
    -- To permit log backups, before the full database backup, modify the database to use the full recovery model.  
    USE master;  
    ALTER DATABASE AdventureWorks2014  
       SET RECOVERY FULL;  
  
    -- Back up the full AdventureWorks2014 database to the container that you created in Lesson 1  
    BACKUP DATABASE AdventureWorks2014   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_onprem.bak'  
  
    ```  
  
4.  打开对象资源管理器并使用存储帐户和帐户密钥连接到 Azure 存储。  
  
5.  展开容器，展开第 1 课中创建的容器，并验证上面步骤 3 中的备份是否出现在此容器中。  
  
    ![本地备份文件在 Azure 容器中显示为 blob](../relational-databases/media/0d060e51-012f-4c61-ab8d-16d461d0ffad.JPG "本地备份文件在 Azure 容器中显示为 blob")  
  
**下一课：**  
  
[第 4 课：将数据库从 URL 还原到虚拟机](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)  
  
