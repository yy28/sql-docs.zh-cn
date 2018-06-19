---
title: 迁移通过 Always Encrypted 保护的敏感数据 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, bulk import
ms.assetid: b2ca08ed-a927-40fb-9059-09496752595e
caps.latest.revision: 11
author: aliceku
ms.author: aliceku
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8e1b17e46097ed7e88651858b571ac86d66ab9d8
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35701778"
---
# <a name="migrate-sensitive-data-protected-by-always-encrypted"></a>迁移通过“始终加密”保护的敏感数据
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
 若要在大容量复制操作期间加载加密数据，而不用在服务器上执行元数据检查，请使用 **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** 选项创建用户。 此选项旨在由早于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] （如 bcp.exe）的 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] 版本的旧式工具使用，或由不能使用“始终加密”的第三方提取-转换-加载 (ETL) 工作流使用。 这使用户可以安全地将加密数据从包含加密列的一组表中移动到具有加密列的另一组表中（在相同或不同的数据库中）。  
 -  
 ## <a name="the-allowencryptedvaluemodifications-option"></a>ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 选项  
 [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) 和 [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) 都具有 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 选项。 当设置为“开”时（默认为“关”），此选项将取消在大容量复制操作中，在服务器上进行的加密元数据检查，以便用户可以在表或数据库之间大容量复制加密数据，而无需解密数据。  
  
## <a name="data-migration-scenarios"></a>数据迁移方案  
下表显示了适用于多个迁移方案的建议设置。  
 
![always-encrypted-migration](../../../relational-databases/security/encryption/media/always-encrypted-migration.PNG "always-encrypted-migration")  

## <a name="bulk-loading-of-encrypted-data"></a>加密数据的大容量加载  
使用以下过程加载加密数据。  

1.  对于作为大容量复制操作目标的数据库中的用户，请将该选项设置为“开”。 例如：  
 
   ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON;  
   ```  

2.  运行大容量复制的应用程序或作为该用户进行连接的工具。 （如果应用程序使用启用了始终加密的客户端驱动程序，请确保数据源的连接字符串不包含 **column encryption setting=enabled** ，以确保从加密列进行检索的数据始终处于加密状态。 有关详细信息，请参阅 [Always Encrypted（客户端开发）](../../../relational-databases/security/encryption/always-encrypted-client-development.md)。）  
  
3.  将 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 选项设置回“关”。 例如：  

    ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = OFF;  
    ```  

## <a name="potential-for-data-corruption"></a>潜在的数据损坏  
错误使用此选项可能导致数据损坏。 **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** 选项使用户可以将任何数据插入数据库中的加密列，包括使用不同密钥进行加密的数据、加密不正确的数据，或根本未加密的数据。 如果用户意外复制了使用为目标列设置的加密方案（列加密密钥、算法、加密类型）进行不正确加密的的数据，则将无法解密数据（数据将损坏）。 请慎用此选项，因为它将导致数据库中的数据损坏。  

下面的方案演示了因错误导入数据而导致数据损坏的方法：  

1.  用户的该选项设置为“开”。  
 
2.  用户运行连接到数据库的应用程序。 应用程序使用大容量 API 将纯文本值插入到加密列中。 应用程序需要启用了始终加密的客户端驱动程序对插入的数据进行加密。 但是，应用程序配置不正确，因此其结果是使用不支持始终加密的驱动程序，或连接字符串不包含 **column encryption setting=enabled**。  

3.  应用程序向服务器发送纯文本值。 由于针对用户在服务器中禁用了加密元数据检查，因此该服务器可让不正确的数据（纯文本而不是正确加密的已加密文本）插入到加密列中。  
 
4.  相同或其他应用程序使用启用了始终加密的驱动程序连接到数据库，并且连接字符串包含 **column encryption setting=enabled** ，并检索了数据。 应用程序要求以透明方式解密数据。 但是，由于数据是错误的密文，因此驱动程序无法解密此数据。  

## <a name="best-practice"></a>最佳实践  
 
针对使用此选项的长时间运行的工作负荷，使用指定的用户帐户。  
 
针对短时间运行的大容量复制应用程序或需要移动加密数据而无需对其进行解密的工具，在运行该应用程序之前，将该选项设置为“开”，并在运行了操作后立即将其设置回“关”。  
 
不要使用此选项开发新应用程序。 而使用可为单个会话提供用于取消加密元数据检查的 API 的客户端驱动程序（如 ADO 4.6.1）。  

## <a name="see-also"></a>另请参阅  
[CREATE USER (Transact-SQL)](../../../t-sql/statements/create-user-transact-sql.md)   
[ALTER USER (Transact-SQL)](../../../t-sql/statements/alter-user-transact-sql.md)   
[Always Encrypted（数据库引擎）](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[始终加密向导](../../../relational-databases/security/encryption/always-encrypted-wizard.md)   
[Always Encrypted（客户端开发）](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  
