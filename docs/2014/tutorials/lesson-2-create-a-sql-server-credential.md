---
title: 第 2 课：创建 SQL Server 凭据 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 64f8805c-1ddc-4c96-a47c-22917d12e1ab
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: fbea11b0500c075105bff885cdb1cd8264b320d6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62931637"
---
# <a name="lesson-2-create-a-sql-server-credential"></a>第 2 课：创建 SQL Server 凭据
  **凭据：**[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 凭据是用于存储连接到 SQL Server 外部资源所需的身份验证信息的对象。  在这里， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份和还原进程使用凭据对 Windows Azure Blob 存储服务进行身份验证。 凭据存储着存储帐户的名称和存储帐户的 **access key** 值。 创建凭据后，在发出 BACKUP/RESTORE 命令时必须在 WITH CREDENTIAL 选项中指定它。 有关如何查看、 复制或重新生成存储帐户详细信息**访问密钥**，请参阅[存储帐户访问密钥](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx)。  
  
 有关凭据的一般信息，请参阅 [凭据](../relational-databases/security/authentication-access/credentials-database-engine.md)。  
  
 有关使用凭据的其他示例的信息，请参阅 [创建 SQL 代理的代理](../ssms/agent/create-a-sql-server-agent-proxy.md)。  
  
> [!IMPORTANT]  
>  创建下文描述的 SQL Server 凭据的要求特定于 SQL Server 的备份过程（[SQL Server Backup to URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)和 [SQL Server Managed  Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)）。 在访问 Azure 存储来读写备份时，SQL Server 使用存储账户名称和访问密钥信息。  有关创建凭据的 Azure 存储中存储数据库文件的详细信息，请参阅[第 3 课：创建 SQL Server 凭据](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="create-a-sql-server-credential"></a>创建 SQL Server 凭据  
 若要创建 SQL Server 凭据，请使用以下步骤：  
  
1.  连接到 SQL Server Management Studio。  
  
2.  在对象资源管理器中，连接到已安装 AdventureWorks2012 数据库的数据库引擎实例，或使用计划用于本教程的自己的数据库。  
  
3.  在 **“标准”** 工具栏上，单击 **“新建查询”**。  
  
4.  将以下示例复制并粘贴到查询窗口中，并根据需要进行修改。  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' - this is the name of the storage account you specified when creating a storage account (See Lesson 1)   
    , SECRET = '<storage account access key>' - this should be either the Primary or Secondary Access Key for the storage account (See Lesson 1)  
  
    ```  
  
     ![存储帐户映射到 sql 凭据](../../2014/tutorials/media/backuptocloud-storage-credential-mapping.gif "映射到 sql 凭据的存储帐户")  
  
5.  验证 T-SQL 语句，然后单击 **“执行”**。  
  
 有关 Windows Azure Blob 存储服务用于备份概念和要求的详细信息，请参阅[Windows Azure Blob 存储服务使用 SQL Server 备份和还原](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
### <a name="next-lesson"></a>下一课  
 [第 3 课：将完整数据库备份写入到 Windows Azure Blob 存储服务](../../2014/tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)。  
  
  
