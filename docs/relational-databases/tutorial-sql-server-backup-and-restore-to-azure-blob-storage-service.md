---
title: 教程：将 SQL Server 备份和还原到 Azure Blob 存储服务 | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 729ec5fc4a811c1c201059ad58086712f6d16f9a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685375"
---
# <a name="tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>教程：将 SQL Server 备份和还原到 Azure Blob 存储服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
本教程介绍如何将备份写入 Azure Blob 存储服务以及如何从中还原。  本教程介绍如何创建 Azure Blob 容器、用于访问存储帐户的凭据，将备份写入 Blob 服务，然后执行简单还原。
  
### <a name="prerequisites"></a>必备条件  
若要完成本教程，你必须熟悉 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份和还原概念以及 T-SQL 语法。 若要使用本教程，需要 Azure 存储帐户、SQL Server Management Studio (SSMS)、针对运行 SQL Server 的服务器的访问权限以及 AdventureWorks 数据库。 此外，用于发出 BACKUP 和 RESTORE 命令的帐户应属于具有“更改任意凭据”权限的 db_backupoperator数据库角色。 

- 获取免费的 [Azure 帐户](https://azure.microsoft.com/offers/ms-azr-0044p/)。
- 创建 [Azure 存储帐户](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=portal)。
- 安装 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安装 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下载 [AdventureWorks2016 示例数据库](https://docs.microsoft.com/sql/samples/adventureworks-install-configure)。
- 将用户帐户分配到 [db_backupoperator](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) 角色，并授予[更改任意凭据](https://docs.microsoft.com/sql/t-sql/statements/alter-credential-transact-sql)权限。 


## <a name="create-azure-blob-container"></a>创建 Azure Blob 容器
容器对 Blob 集进行分组。 所有 Blob 必须都在一个容器中。 一个帐户可以包含无限数量的容器，但必须至少具有一个容器。 一个容器可以存储无限数量的 Blob。 

若要创建容器，请执行下列步骤：

1. 打开 Azure 门户。 
1. 导航到你的存储帐户。 
   1. 选择该存储帐户，向下滚动到“Blob 服务”。
   1. 选择“Blob”，然后选择“+容器”以添加一个新容器。 
   1. 输入容器名称并记下指定的容器名称。 此信息用在本教程后面的 T-SQL 语句的 URL（备份文件的路径）中。 
   1. 选择“确定”。 
    
    ![新建容器](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/new-container.png)


  >[!NOTE]
  >即使选择创建公共容器，SQL Server 备份和还原仍需要对存储帐户进行身份验证。 还可以使用 REST API 以编程方式创建容器。 有关详细信息，请参阅[创建容器](https://docs.microsoft.com/rest/api/storageservices/Create-Container)


## <a name="create-a-sql-server-credential"></a>创建 SQL Server 凭据
SQL Server 凭据是一个对象，用于存储连接到 SQL Server 以外资源所需的身份验证信息。 在此处，SQL Server 备份和还原进程使用凭据对 Windows Azure Blob 存储服务进行身份验证。 凭据存储着存储帐户的名称和存储帐户的 **access key** 值。 创建凭据后，在发出 BACKUP/RESTORE 命令时必须在 WITH CREDENTIAL 选项中指定它。 有关凭据的详细信息，请参阅[凭据](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/credentials-database-engine)。 

  >[!IMPORTANT]
  >创建下文描述的 SQL Server 凭据的要求特定于 SQL Server 的备份过程（[SQL Server 备份到 URL](backup-restore/sql-server-backup-to-url.md) 和 [Microsoft Azure 的 SQL Server 托管备份](backup-restore/sql-server-managed-backup-to-microsoft-azure.md)）。 SQL Server 在访问 Azure 存储来读写备份时，使用存储帐户名称和访问密钥信息。

### <a name="access-keys"></a>访问密钥
由于 Azure 门户仍处于打开状态，请保存创建凭据所需的访问密钥。 

1. 导航到 Azure 门户中的“存储帐户”。 
1. 向下滚动到“设置”，然后选择“访问密钥”。 
1. 保存密钥和连接字符串以在本教程后面使用。 

   ![访问密钥](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/access-keys.png)

### <a name="create-a-sql-server-credential"></a>创建 SQL Server 凭据
使用保存的访问密钥，按照以下步骤创建 SQL Server 凭据。 

1. 使用 SQL Server Management Studio 连接到 SQL Server。 
1. 选择“AdventureWorks2016”数据库，打开“新建查询”窗口。 
1. 将以下示例复制、粘贴到查询窗口并在其中执行，根据需要进行修改： 

  ```sql
  CREATE CREDENTIAL mycredential   
  WITH IDENTITY= 'mystorageaccount', -- this is the name of the storage account you specified when creating a storage account   
  SECRET = '<storage account access key>' -- this should be either the Primary or Secondary Access Key for the storage account 
  ```
1. 执行该语句以创建凭据。 

## <a name="backup-database-to-the-windows-azure-blob-storage-service"></a>将数据库备份到 Windows Azure Blob 存储服务
在本部分中，将使用 T-SQL 语句执行到 Windows Azure Blob 存储服务的完整数据库备份。 

1. 使用 SQL Server Management Studio 连接到 SQL Server。 
1. 选择“AdventureWorks2016”数据库，打开“新建查询”窗口。 
1. 将以下示例复制并粘贴到查询窗口中，根据需要进行修改： 

 ```sql
 BACKUP DATABASE[AdventureWorks2016] 
 TO URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2016.bak' 
 /* URL includes the endpoint for the BLOB service, followed by the container name, and the name of the backup file*/ 
 WITH CREDENTIAL = 'mycredential';
 /* name of the credential you created in the previous step */ 
 GO
 ```
1. 执行该语句以将 AdventureWorks2016 数据库备份到 URL。 

 
## <a name="restore-database-from-windows-azure-blob-storage-service"></a>从 Windows Azure Blob 存储服务还原数据库
在本部分中，将使用 T-SQL 语句以还原完整数据库备份。 

1. 使用 SQL Server Management Studio 连接到 SQL Server。 
1. 打开“新建查询”窗口。 
1. 将以下示例复制并粘贴到查询窗口中，根据需要进行修改： 

 ```sql
 RESTORE DATABASE AdventureWorks2016 
 FROM URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak' 
 WITH CREDENTIAL = 'mycredential',
 STATS = 5 -- use this to see monitor the progress
 GO
 ``` 

## <a name="see-also"></a>另请参阅 
以下是一些建议阅读的主题，便于了解概念以及在将 Azure Blob 存储服务用于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份时的最佳做法。  
  
-   [使用 Microsoft Azure Blob 存储服务进行 SQL Server 备份和还原](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
-   [SQL Server 备份到 URL 最佳实践和故障排除](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
