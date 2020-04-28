---
title: 第3课：创建 SQL Server 凭据 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 61a25d1f4e86204d05b3be6bf2a5dbc8cd0474b9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "70153835"
---
# <a name="lesson-3-create-a-sql-server-credential"></a>第 3 课：创建 SQL Server 凭据
  在本课中，您将创建凭据以存储用于访问 Azure 存储帐户的安全信息。  
  
 SQL Server 凭据是一个对象，用于存储连接到 SQL Server 以外资源所需的身份验证信息。 凭据中存储了存储容器的 URI 路径以及共享的访问签名密钥值。 对于数据或日志文件使用的每个存储容器，都必须创建一个 SQL Server 凭据，其名称与容器路径相同。  
  
 有关凭据的一般信息，请参阅[凭据 &#40;数据库引擎&#41;](security/authentication-access/credentials-database-engine.md)。  
  
> [!IMPORTANT]  
>  创建下述 SQL Server 凭据的要求特定于[Azure 功能中的 SQL Server 数据文件](databases/sql-server-data-files-in-microsoft-azure.md)。 有关在 Azure 存储中创建备份过程的凭据的信息，请参阅 [Lesson 2: Create a SQL Server Credential](../tutorials/lesson-2-create-a-sql-server-credential.md)。  
  
 若要创建 SQL Server 凭据，请执行以下步骤：  
  
1.  连接到 SQL Server Management Studio。  
  
2.  在对象资源管理器中，连接到所安装的数据库引擎实例。  
  
3.  在“标准”工具栏上，单击“新建查询”。  
  
4.  将以下示例复制并粘贴到查询窗口中，并根据需要进行修改。 以下语句将创建一个 SQL Server 凭据来存储存储容器的共享访问证书。  
  
    ```sql  
  
    USE master  
    CREATE CREDENTIAL credentialname - this name should match the container path and it must start with https.   
       WITH IDENTITY='SHARED ACCESS SIGNATURE', -- this is a mandatory string and do not change it.   
       SECRET = 'sharedaccesssignature' -- this is the shared access signature key that you obtained in Lesson 2.   
    GO  
  
    ```  
  
     有关详细信息，请参阅 SQL Server 联机丛书中的[CREATE CREDENTIAL &#40;transact-sql&#41;](/sql/t-sql/statements/create-credential-transact-sql) 。  
  
5.  若要查看所有可用的凭据，可在查询窗口中运行以下语句：  
  
    ```sql  
    SELECT * from sys.credentials  
    ```  
  
     有关 sys.databases 的详细信息，请参阅 SQL Server 联机丛书中的[sys.databases &#40;transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) 。  
  
 **下一课：**  
  
 [第 4 课：在 Azure 存储中创建数据库](lesson-3-database-backup-to-url.md)  
  
  
