---
title: 在两个服务器上创建相同的对称密钥 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- symmetric keys [SQL Server], creating
ms.assetid: a13d0b21-a43b-43c0-9c22-7ba8f3d15e80
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 85901ba63607de721259431ab83d3a0cd3a3185d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011714"
---
# <a name="create-identical-symmetric-keys-on-two-servers"></a>在两个服务器上创建相同的对称密钥
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中的两台不同的服务器上创建相同的对称密钥。 为了对密码进行解密，需要用于加密密码的密钥。 在一个数据库中同时执行加密和解密时，密钥保存在数据库中并可同时用于（取决于权限）加密和解密。 但在不同的数据库或服务器中执行加密和解密时，保存在一个数据库中的密钥不能用于另一数据库。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   [使用 Transact-SQL 在两台不同的服务器上创建相同的对称密钥](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   创建对称密钥时，必须至少使用以下项之一来对该对称密钥进行加密：证书、密码、对称密钥、非对称密钥或 PROVIDER。 可使用上述每种类型中的多项对密钥进行加密。 换言之，可以同时使用多个证书、密码、对称密钥以及非对称密钥对单个对称密钥进行加密。  
  
-   当使用密码（而不是数据库主密钥的公钥）对对称密钥进行加密时，便会使用 TRIPLE DES 加密算法。 因此，用强加密算法（如 AES）创建的密钥本身受较弱算法的保护。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求对数据库具有 ALTER ANY SYMMETRIC KEY 权限。 如果指定了 AUTHORIZATION，则要求对数据库用户具有 IMPERSONATE 权限，或者对应用程序角色具有 ALTER 权限。 如果使用证书或非对称密钥进行加密，则要求对证书或非对称密钥具有 VIEW DEFINITION 权限。 只有 Windows 登录名、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名和应用程序角色才能拥有对称密钥。 其他组和角色不能拥有对称密钥。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-identical-symmetric-keys-on-two-different-servers"></a>在两台不同的服务器上创建相同的对称密钥  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  通过运行以下 CREATE MASTER KEY、CREATE CERTIFICATE 和 CREATE SYMMETRIC KEY 语句来创建密钥。  
  
    ```  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'My p@55w0Rd';  
    GO  
    CREATE CERTIFICATE [cert_keyProtection] WITH SUBJECT = 'Key Protection';  
    GO  
    CREATE SYMMETRIC KEY [key_DataShare] WITH  
        KEY_SOURCE = 'My key generation bits. This is a shared secret!',  
        ALGORITHM = AES_256,   
        IDENTITY_VALUE = 'Key Identity generation bits. Also a shared secret'  
        ENCRYPTION BY CERTIFICATE [cert_keyProtection];  
    GO  
    ```  
  
4.  连接到一个独立的服务器实例，打开不同的查询窗口，然后运行上述 SQL 语句来在另一台服务器上创建相同的密钥。  
  
5.  先在第一台服务器上运行以下 OPEN SYMMETRIC KEY 语句和 SELECT 语句，以测试密钥。  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    SELECT encryptbykey(key_guid('key_DataShare'), 'MyData' )  
    GO  
    -- For example, the output might look like this: 0x2152F8DA8A500A9EDC2FAE26D15C302DA70D25563DAE7D5D1102E3056CE9EF95CA3E7289F7F4D0523ED0376B155FE9C3  
    ```  
  
6.  在另一服务器上，将上一个 SELECT 语句的结果作为 `@blob` 的值粘贴到以下代码中，并运行以下代码以验证复制的密钥可对密码进行解密。  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    DECLARE @blob varbinary(8000);  
    SET @blob = SELECT CONVERT(varchar(8000), decryptbykey(@blob));  
    GO  
    ```  
  
7.  在两个服务器上关闭对称密钥。  
  
    ```  
    CLOSE SYMMETRIC KEY [key_DataShare];  
    GO  
    ```  
  
 有关详细信息，请参见以下内容：  
  
-   [CREATE MASTER KEY (Transact-SQL)](/sql/t-sql/statements/create-master-key-transact-sql)  
  
-   [CREATE CERTIFICATE (Transact-SQL)](/sql/t-sql/statements/create-certificate-transact-sql)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)  
  
-   [ENCRYPTBYKEY (Transact-SQL)](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [DECRYPTBYKEY (Transact-SQL)](/sql/t-sql/functions/decryptbykey-transact-sql)  
  
-   [OPEN SYMMETRIC KEY (Transact-SQL)](/sql/t-sql/statements/open-symmetric-key-transact-sql)  
  
  
