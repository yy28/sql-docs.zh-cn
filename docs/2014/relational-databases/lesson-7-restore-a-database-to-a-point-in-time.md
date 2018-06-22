---
title: 第 8 课. 将数据库还原到 Windows Azure 存储空间 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ea9ec20e60fb879b17434e8fe4581d28b3d7a551
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015671"
---
# <a name="lesson-8-restore-a-database-to-windows-azure-storage"></a>第 8 课. 将数据库还原到 Windows Azure 存储
  在本课中，您将学习如何在本地创建备份文件，然后将其还原到 Windows Azure 存储。 注意，数据库可在本地，也可在 Windows Azure 的虚拟机中。 不需要学完第 4、5、6 和 7 课即可听懂本课。  
  
 本课假定您已完成以下步骤：  
  
-   具有 Windows Azure 存储帐户。  
  
-   已在 Windows Azure 存储帐户下创建了容器。  
  
-   已在容器上创建了具有读取、写入和列表权限的策略。 还生成了 SAS 密钥。  
  
-   已根据共享访问签名在源计算机上创建了 SQL Server 凭据。  
  
-   已在源计算机中创建了数据库。  
  
 若要将数据库还原到 Windows Azure 存储，可执行以下步骤：  
  
1.  在源计算机中，启动 SQL Server Management Studio。  
  
2.  连接到新创建的数据库时，打开查询窗口。 运行以下语句：  
  
    ```tsql  
  
    USE TestDB3Restore;   
    GO   
    BACKUP DATABASE TestDB3Restore   
    TO DISK = 'C:\BACKUP\TestDB3Restore.Bak'   
       WITH FORMAT,   
       NAME = 'Full Backup of TestDB3Restore'   
    GO  
  
    ```  
  
3.  接下来，将以下语句复制到查询窗口中并运行这些语句。  
  
    ```tsql  
  
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
  
 若要使用 SQL Server Management Studio 用户界面通过指向 Windows Azure 存储的数据和日志文件还原数据库，请执行以下步骤：  
  
1.  在**对象资源管理器**，单击服务器名称以展开服务器树。  
  
2.  展开**数据库**，然后选择你的数据库。  
  
3.  右键单击数据库，指向“任务”，再单击“还原”。  
  
4.  上**常规**页上，在**还原**源部分，单击**源**设备。  
  
5.  单击浏览按钮**源**设备文本框中，这将打开**选择备份设备**对话框。  
  
6.  在备份媒体文本框中，选择**文件**，然后单击**添加**按钮以找到备份 (.bak) 文件。 单击“确定” 。  
  
7.  单击**文件**第一页上。  
  
8.  在**还原数据库文件**一样部分下,**还原为**字段中，键入以下内容：  
  
     对于数据文件，请键入： `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS.mdf`。 对于日志文件，请键入： `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS_log.ldf`。  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-8.gif "SQL 14 CTP2")  
  
9. 单击“确定” 。  
  
 还原完后，登录到管理门户。 应该能在容器中看到 .mdf 和 .ldf 文件，如下所示：  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-9.gif "SQL 14 CTP2")  
  
 **下一课：**  
  
 [第 9 课.从 Microsoft Azure 存储还原数据库](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  