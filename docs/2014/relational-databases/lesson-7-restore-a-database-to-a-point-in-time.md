---
title: 第 8 课. 将数据库还原到 Azure 存储 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5b30a9f60f52b8b19875f5fb3c15242ce2c632fd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "70175426"
---
# <a name="lesson-8-restore-a-database-to-azure-storage"></a>第 8 课. 将数据库还原到 Azure 存储
  在本课中，您将学习如何在本地创建备份文件，然后将其还原到 Azure 存储。 请注意，你可以在本地或 Azure 中的虚拟机上使用数据库。 不需要学完第 4、5、6 和 7 课即可听懂本课。  
  
 本课假定您已完成以下步骤：  
  
-   你有 Azure 存储帐户。  
  
-   在 Azure 存储帐户下创建了容器。  
  
-   已在容器上创建了具有读取、写入和列表权限的策略。 还生成了 SAS 密钥。  
  
-   已根据共享访问签名在源计算机上创建了 SQL Server 凭据。  
  
-   已在源计算机中创建了数据库。  
  
 若要将数据库还原到 Azure 存储，可执行以下步骤：  
  
1.  在源计算机中，启动 SQL Server Management Studio。  
  
2.  连接到新创建的数据库时，打开查询窗口。 运行以下语句：  
  
    ```sql  
  
    USE TestDB3Restore;   
    GO   
    BACKUP DATABASE TestDB3Restore   
    TO DISK = 'C:\BACKUP\TestDB3Restore.Bak'   
       WITH FORMAT,   
       NAME = 'Full Backup of TestDB3Restore'   
    GO  
  
    ```  
  
3.  接下来，将以下语句复制到查询窗口中并运行这些语句。  
  
    ```sql  
  
    USE master;   
    GO   
    RESTORE DATABASE TestDB3Restore    
    FROM DISK = 'C:\BACKUP\TestDB3Restore.bak'    
    WITH REPLACE,   
    MOVE 'TestDB3Restore' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore.mdf',     
    MOVE 'TestDB3Restore_log' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore_log.ldf';   
    GO  
  
    ```  
  
     在此步骤结束时，您的容器应在管理门户上列出数据 (.mdf) 和 (.ldf) 文件。  
  
 若要使用 SQL Server Management Studio 用户界面还原包含指向 Azure 存储的数据文件和日志文件的数据库，请执行以下步骤：  
  
1.  在**对象资源管理器**中，单击服务器名称以展开服务器树。  
  
2.  展开 "**数据库**"，然后选择数据库。  
  
3.  右键单击数据库，指向“任务”****，再单击“还原”****。  
  
4.  在 "**常规**" 页上的 "**还原**源" 部分中，单击 "**源**设备"。  
  
5.  单击 "**源**设备" 文本框的浏览按钮，这将打开 "**选择备份设备**" 对话框。  
  
6.  在 "备份介质" 文本框中，选择 "**文件**"，然后单击 "**添加**" 按钮以找到备份（.bak）文件。 单击“确定”。   
  
7.  在第一页上单击 "**文件**"。  
  
8.  在 "将**数据库文件还原**为" 部分中的 "**还原为**" 字段下，键入以下内容：  
  
     对于数据文件，键入： `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS.mdf`。 对于日志文件，键入： `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS_log.ldf`。  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-8.gif "SQL 14 CTP2")  
  
9. 单击“确定”。   
  
 还原完后，登录到管理门户。 应该能在容器中看到 .mdf 和 .ldf 文件，如下所示：  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-9.gif "SQL 14 CTP2")  
  
 **下一课：**  
  
 [第9课：从 Azure 存储还原数据库](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
