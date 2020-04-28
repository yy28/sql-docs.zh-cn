---
title: 第7课：将数据文件移到 Azure 存储 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 25ae3cee8e08292297449914bfb6e40dfc1b4b3a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "70175462"
---
# <a name="lesson-7-move-your-data-files-to-azure-storage"></a>第 7 课：将数据文件移动到 Azure 存储
  在本课中，您将学习如何将数据文件移到 Azure 存储（而不是您的 SQL Server 实例）中。 不需要学完第 4、5 和 6 课即可听懂本课。  
  
 若要将数据文件移到 Azure 存储，可以使用`ALTER DATABASE`语句，因为它可帮助更改数据文件的位置。  
  
 本课假定您已完成以下步骤：  
  
-   你有 Azure 存储帐户。  
  
-   在 Azure 存储帐户下创建了容器。  
  
-   已在容器上创建了具有读取、写入和列表权限的策略。 还生成了 SAS 密钥。  
  
-   已在源计算机上创建了 SQL Server 凭据。  
  
 接下来，使用以下步骤将数据文件移到 Azure 存储：  
  
1.  首先，在源计算机中创建测试数据库，然后向其添加一些数据。  
  
    ```sql  
  
    USE master;   
    CREATE DATABASE TestDB1Alter;   
    GO   
    USE TestDB1Alter;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO  
  
    ```  
  
2.  运行以下代码：  
  
    ```sql  
  
    -- In the following statement, modify the path specified in FILENAME to   
    -- the new location of the file in Azure Storage container.   
    ALTER DATABASE TestDB1Alter    
        MODIFY FILE ( NAME = TestDB1Alter,    
                    FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontaineralter/TestDB1AlterData.mdf');   
    GO  
  
    ```  
  
3.  当你运行此操作时，你将看到以下消息： "文件" Testdb1alter ' "已在系统目录中修改。 新路径将在数据库下次启动时使用。 "  
  
4.  然后，将数据库设为脱机状态。  
  
    ```sql  
  
    ALTER DATABASE TestDB1Alter SET OFFLINE;   
    GO  
  
    ```  
  
5.  现在，需要使用以下方法之一将数据文件复制到 Azure 存储： [AzCopy 工具](https://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)、 [Put 页面](https://msdn.microsoft.com/library/azure/ee691975.aspx)、[存储客户端库参考](https://msdn.microsoft.com/library/azure/dn261237.aspx)或第三方存储资源管理器工具。  
  
     **重要提示：** 使用此新增强功能时，请始终确保创建的是页 Blob 而非块 Blob。  
  
6.  然后，将数据库设为联机状态。  
  
    ```sql  
  
    ALTER DATABASE TestDB1Alter SET ONLINE;   
    GO  
  
    ```  
  
 **下一课：**  
  
 [第8课。将数据库还原到 Azure 存储](lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
