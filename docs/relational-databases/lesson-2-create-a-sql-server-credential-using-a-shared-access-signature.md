---
title: 第 2 课：使用共享访问签名创建 SQL Server 凭据 | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
caps.latest.revision: 17
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 555f26b131b56984279f3a6e79ef5c70373b680d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-2-create-a-sql-server-credential-using-a-shared-access-signature"></a>第 2 课：使用共享访问签名创建 SQL Server 凭据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在本课中，将创建一个用于存储安全信息的凭据，SQL Server 将使用这些信息对在 [第 1 课：在 Azure 容器上创建存储访问策略和共享访问签名](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)中创建的 Azure 容器中执行写入和读取操作。  
  
SQL Server 凭据是一个对象，用于存储连接到 SQL Server 以外资源所需的身份验证信息。 凭据中存储了存储容器的 URI 路径以及此容器的共享访问签名。  
  
> [!NOTE]  
> 如果要将 SQL Server 2012 SP1 CU2 或更高版本数据库或 SQL Server 2014 数据库备份到此 Azure 容器，可以使用此处记录的 [已弃用语法](https://technet.microsoft.com/en-US/library/dn435916(v=sql.120).aspx) ，基于存储帐户密钥创建 SQL Server 凭据。  
  
## <a name="create-sql-server-credential"></a>创建 SQL Server 凭据  
若要创建 SQL Server 凭据，请执行以下步骤：  
  
1.  连接到 SQL Server Management Studio。  
  
2.  打开一个新查询窗口，然后连接到本地环境中数据引擎的 SQL Server 2016 实例。  
  
3.  在新查询窗口中，粘贴 CREATE CREDENTIAL 语句以及第 1 课中的共享访问签名，然后执行该脚本。  
  
    该脚本将类似如下代码。  
  
    ```Transact-SQL  
  
    USE master  
    CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] -- this name must match the container path, start with https and must not contain a forward slash.  
       WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
       , SECRET = 'sharedaccesssignature' -- this is the shared access signature key that you obtained in Lesson 1.   
    GO  
  
    ```  
  
4.  若要查看所有可用的凭据，可在连接到实例的查询窗口中运行以下语句：  
  
    ```Transact-SQL  
    SELECT * from sys.credentials  
    ```  
  
5.  打开一个新查询窗口，然后连接到 Azure 虚拟机中的数据库引擎的 SQL Server 2016 实例。  
  
6.  在新查询窗口中，粘贴 CREATE CREDENTIAL 语句以及第 1 课中的共享访问签名，然后执行该脚本。  
  
7.  对想要为其提供 Azure 容器访问权限的任何其他 SQL Server 2016 实例重复执行步骤 5 和 6。  
  
**下一课：**  
  
[第 3 课：将数据库备份到 URL](../relational-databases/lesson-3-database-backup-to-url.md)  
  
## <a name="see-also"></a>另请参阅  
[凭据（数据库引擎）](../relational-databases/security/authentication-access/credentials-database-engine.md)  
[CREATE CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-credential-transact-sql.md)  
[sys.credentials (Transact-SQL)](../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  

