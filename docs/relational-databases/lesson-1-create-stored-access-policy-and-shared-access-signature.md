---
title: 第 1 课：创建存储访问策略和共享访问签名 | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: 41674d9d-8132-4bff-be4d-85a861419f3d
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 721f9245ff8057c54cef5facdf4a4de423e53961
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-create-stored-access-policy-and-shared-access-signature"></a>第 1 课：创建存储访问策略和共享访问签名
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
本课程将介绍如何通过使用存储访问策略使用 [Azure PowerShell](https://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/) 脚本在 Azure blob 容器上创建共享访问签名。  
  
> [!NOTE]  
> 该脚本是使用 Azure PowerShell 5.0.10586 编写的。  
  
共享访问签名是一个 URI，它授予对容器、Blob、队列或表的受限访问权限。 存储访问策略在服务器端的共享访问签名之外又增加了一级控制，包括撤消、终止或扩展访问。 使用此项新增强时，需要在容器上创建至少具有读取、写入和列表权限的策略。  
  
可以使用 Azure PowerShell、Azure Storage SDK、Azure REST API 或第三方实用程序创建存储访问策略和共享访问签名。 本教程演示了如何使用 Azure PowerShell 脚本来完成此任务。 该脚本使用资源管理器部署模型并创建以下新资源  
  
-   资源组 (Resource group)  
  
-   存储帐户  
  
-   Azure blob 容器  
  
-   SAS 策略  
  
此脚本首先通过声明一些变量以指定以上资源的名称和以下必需的输入值的名称：  
  
-   用于命名其他资源对象的前缀名称  
  
-   订阅名称  
  
-   数据中心位置  
  
> [!NOTE]  
> 以此方式编写此脚本，使你可以使用现有的 ARM 或经典部署模型资源。  
  
通过生成适当的 CREATE CREDENTIAL 语句完成此脚本，此语句将在 [第 2 课：使用共享访问签名创建 SQL Server 凭据](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)中进行介绍。 此语句已被复制到剪贴板，并将输出到控制台供你使用。  
  
要在容器上创建策略并生成共享访问签名 (SAS) 密钥，请按照以下步骤：  
  
1.  打开 Window PowerShell 或 Windows PowerShell ISE（请参阅以上版本要求）。  
  
2.  编辑，然后执行以下脚本。  
  
    ```  
    <#   
    This script uses the Azure Resource model and creates a new ARM storage account.  
    Modify this script to use an existing ARM or classic storage account   
    using the instructions in comments within this script  
    #>  
    # Define global variables for the script  
    $prefixName = '<a prefix name>'  # used as the prefix for the name for various objects  
    $subscriptionName='<your subscription name>'   # the name  of subscription name you will use  
    $locationName = '<a data center location>'  # the data center region you will use  
    $storageAccountName= $prefixName + 'storage' # the storage account name you will create or use  
    $containerName= $prefixName + 'container'  # the storage container name to which you will attach the SAS policy with its SAS token  
    $policyName = $prefixName + 'policy' # the name of the SAS policy  
  
    <#   
    Using Azure Resource Manager deployment model  
    Comment out this entire section and use the classic storage account name to use an existing classic storage account  
    #>  
  
    # Set a variable for the name of the resource group you will create or use  
    $resourceGroupName=$prefixName + 'rg'   
  
    # adds an authenticated Azure account for use in the session   
    Login-AzureRmAccount    
  
    # set the tenant, subscription and environment for use in the rest of   
    Set-AzureRmContext -SubscriptionName $subscriptionName   
  
    # create a new resource group - comment out this line to use an existing resource group  
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $locationName   
  
    # Create a new ARM storage account - comment out this line to use an existing ARM storage account  
    New-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $resourceGroupName -Type Standard_RAGRS -Location $locationName   
  
    # Get the access keys for the ARM storage account  
    $accountKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName  
  
    # Create a new storage account context using an ARM storage account  
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $accountKeys[0].Value 
  
    <#  
    Using the Classic deployment model  
    Use the following four lines to use an existing classic storage account  
    #>  
    #Classic storage account name  
    #Add-AzureAccount  
    #Select-AzureSubscription -SubscriptionName $subscriptionName #provide an existing classic storage account  
    #$accountKeys = Get-AzureStorageKey -StorageAccountName $storageAccountName  
    #$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $accountKeys.Primary  
  
    # The remainder of this script works with either the ARM or classic sections of code above  
  
    # Creates a new container in blob storage  
    $container = New-AzureStorageContainer -Context $storageContext -Name $containerName  
  
    # Sets up a Stored Access Policy and a Shared Access Signature for the new container  
    $policy = New-AzureStorageContainerStoredAccessPolicy -Container $containerName -Policy $policyName -Context $storageContext -StartTime $(Get-Date).ToUniversalTime().AddMinutes(-5) -ExpiryTime $(Get-Date).ToUniversalTime().AddYears(10) -Permission rwld

    # Gets the Shared Access Signature for the policy  
    $sas = New-AzureStorageContainerSASToken -name $containerName -Policy $policyName -Context $storageContext
    Write-Host 'Shared Access Signature= '$($sas.Substring(1))''  
  
    # Outputs the Transact SQL to the clipboard and to the screen to create the credential using the Shared Access Signature  
    Write-Host 'Credential T-SQL'  
    $tSql = "CREATE CREDENTIAL [{0}] WITH IDENTITY='Shared Access Signature', SECRET='{1}'" -f $cbc.Uri,$sas.Substring(1)   
    $tSql | clip  
    Write-Host $tSql  
  
    ```  
  
3.  脚本完成后，CREATE CREDENTIAL 语句将位于剪贴板中，以便在下一课中使用。  
  
**下一课：**  
  
[第 2 课：使用共享访问签名创建 SQL Server 凭据](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="see-also"></a>另请参阅  
[共享访问签名，第 1 部分：了解 SAS 模型](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
[Create Container](https://msdn.microsoft.com/library/azure/dd179468.aspx)  
[Set Container ACL](https://msdn.microsoft.com/library/azure/dd179391.aspx)  
[Get Container ACL](https://msdn.microsoft.com/library/azure/dd179469.aspx)  
  
  
  

