---
title: 第 2 课。 在容器上创建策略并生成共享访问签名 (SAS) 密钥 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 41674d9d-8132-4bff-be4d-85a861419f3d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 23e80a2bf02ee6b97449ea3acff38a3937d37000
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "67046735"
---
# <a name="lesson-2-create-a-policy-on-container-and-generate-a-shared-access-signature-sas-key"></a>第 2 课。 在容器上创建策略并生成共享访问签名 (SAS) 密钥
  在本课中，您将学习如何在 Blob 容器上创建策略以及生成 SAS 密钥。  
  
 存储的访问策略在服务器端的共享访问签名之外又增加了一级控制。 共享访问签名是一个 URI，它授予对容器、Blob、队列和表的受限访问权限。 使用此项新增强时，需要在容器上创建具有读取、写入和列表权限的策略。  
  
 可使用以下某种方法创建策略和共享访问签名：  
  
-   Windows Azure REST API 操作：[创建容器](https://msdn.microsoft.com/library/azure/dd179468.aspx)，[设置容器 ACL](https://msdn.microsoft.com/library/azure/dd179391.aspx)，和[获取容器 ACL](https://msdn.microsoft.com/library/azure/dd179469.aspx)。  
  
-   Windows Azure SDK 中的[CloudBlobContainer.GetSharedAccessSignature 方法](https://docs.microsoft.com/dotnet/api/microsoft.azure.storage.blob.cloudblobcontainer.getsharedaccesssignature) 。  
  
    ```  
  
       string signature = blob.GetSharedAccessSignature(new SharedAccessPolicy()   
        {   
            // Specify the expiration time for the signature.   
            SharedAccessExpiryTime = DateTime.Now.Years(1),   
            // Specify the permissions granted by the signature.    
            Permissions = SharedAccessPermissions.Write | SharedAccessPermissions.Read   
        });  
  
    ```  
  
-   第三方 Windows Azure 资源管理器工具，如 [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/)。  
  
 **下一课：**  
  
 [第 3 课：创建 SQL Server 凭据](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
  
