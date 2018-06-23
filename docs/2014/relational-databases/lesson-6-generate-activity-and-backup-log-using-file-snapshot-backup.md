---
title: 第 7 课： 将数据文件移动到 Windows Azure 存储空间 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 014fd10ecd738f46160358506b3b165640d3fe09
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015223"
---
# <a name="lesson-7-move-your-data-files-to-windows-azure-storage"></a>第 7 课：将数据文件移动到 Windows Azure 存储
  在本课中，您将学习如何将数据文件移至 Windows Azure 存储（但不移至 SQL Server 实例）。 不需要学完第 4、5 和 6 课即可听懂本课。  
  
 若要将数据文件移至 Windows Azure 存储，您可以使用 `ALTER DATABASE` 语句，因为它可帮助更改数据文件的位置。  
  
 本课假定您已完成以下步骤：  
  
-   具有 Windows Azure 存储帐户。  
  
-   已在 Windows Azure 存储帐户下创建了容器。  
  
-   已在容器上创建了具有读取、写入和列表权限的策略。 还生成了 SAS 密钥。  
  
-   已在源计算机上创建了 SQL Server 凭据。  
  
 接下来，按照以下步骤将数据文件移至 Windows Azure 存储：  
  
1.  首先，在源计算机中创建测试数据库，然后向其添加一些数据。  
  
    ```tsql  
  
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
  
    ```tsql  
  
    -- In the following statement, modify the path specified in FILENAME to   
    -- the new location of the file in Windows Azure Storage container.   
    ALTER DATABASE TestDB1Alter    
        MODIFY FILE ( NAME = TestDB1Alter,    
                    FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontaineralter/TestDB1AlterData.mdf');   
    GO  
  
    ```  
  
3.  运行此代码时，你将看到此消息：“已在系统目录中修改了文件‘TestDB1Alter’”。 新路径将在数据库下次启动时使用。”  
  
4.  然后，将数据库设为脱机状态。  
  
    ```tsql  
  
    ALTER DATABASE TestDB1Alter SET OFFLINE;   
    GO  
  
    ```  
  
5.  现在，你需要使用以下方法之一将数据文件复制到 Windows Azure 存储： [AzCopy 工具](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)、 [放置页](https://msdn.microsoft.com/library/azure/ee691975.aspx)、 [存储客户端库参考](https://msdn.microsoft.com/library/azure/dn261237.aspx)或第三方存储资源管理器工具。  
  
     **重要提示：** 使用此新增强功能时，请始终确保创建的是页 Blob 而非块 Blob。  
  
6.  然后，将数据库设为联机状态。  
  
    ```tsql  
  
    ALTER DATABASE TestDB1Alter SET ONLINE;   
    GO  
  
    ```  
  
 **下一课：**  
  
 [第 8 课：将数据库还原到 Microsoft Azure 存储](lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  