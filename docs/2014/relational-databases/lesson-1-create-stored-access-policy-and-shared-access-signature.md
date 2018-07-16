---
title: 第 2 课。 在容器上创建策略并生成共享访问签名 (SAS) 密钥 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 41674d9d-8132-4bff-be4d-85a861419f3d
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 708c347e587d19ebfb7c2f24e94fd59db0289c52
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37324297"
---
# <a name="lesson-2-create-a-policy-on-container-and-generate-a-shared-access-signature-sas-key"></a>第 2 课。 在容器上创建策略并生成共享访问签名 (SAS) 密钥
  在本课中，您将学习如何在 Blob 容器上创建策略以及生成 SAS 密钥。  
  
 存储的访问策略在服务器端的共享访问签名之外又增加了一级控制。 共享访问签名是一个 URI，它授予对容器、Blob、队列和表的受限访问权限。 使用此项新增强时，需要在容器上创建具有读取、写入和列表权限的策略。  
  
 可使用以下某种方法创建策略和共享访问签名：  
  
-   Windows Azure REST API 操作： [创建容器](https://msdn.microsoft.com/library/azure/dd179468.aspx)、 [设置容器 ACL](https://msdn.microsoft.com/library/azure/dd179391.aspx)和 [获取容器 ACL](https://msdn.microsoft.com/library/azure/dd179469.aspx)。  
  
-   Windows Azure SDK 中的[CloudBlobContainer.GetSharedAccessSignature 方法](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storageclient.cloudblobcontainer.getsharedaccesssignature.aspx) 。  
  
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
  
  
