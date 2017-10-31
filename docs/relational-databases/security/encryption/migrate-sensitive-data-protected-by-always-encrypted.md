---
title: "迁移通过 Always Encrypted 保护的敏感数据 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/04/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Always Encrypted, bulk import
ms.assetid: b2ca08ed-a927-40fb-9059-09496752595e
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 20eb76a9e2cc89015167b5199f1a6f8dd5baec16
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="migrate-sensitive-data-protected-by-always-encrypted"></a>迁移通过“始终加密”保护的敏感数据
 <a name="to-load-encrypted-data-without-performing-metadata-checks-on-the-server-during-bulk-copy-operations-create-the-user-with-the-allowencryptedvaluemodifications-option-this-option-is-intended-to-be-used-by-legacy-tools-from-versions-of-includessnoversionincludesssnoversion-mdmd-older-than-includesssql15includessssql15-mdmd-such-as-bcpexe-or-by-using-third-party-extract-transform-load-etl-work-flows-that-cannot-use-always-encrypted-this-allows-a-user-to-securely-move-encrypted-data-from-one-set-of-tables-containing-encrypted-columns-to-another-set-of-tables-with-encrypted-columns-in-the-same-or-a-different-database"></a>若要在大容量复制操作期间加载加密数据，而不用在服务器上执行元数据检查，请使用 **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** 选项创建用户。 此选项旨在由早于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] （如 bcp.exe）的 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] 版本的旧式工具使用，或由不能使用“始终加密”的第三方提取-转换-加载 (ETL) 工作流使用。 这使用户可以安全地将加密数据从包含加密列的一组表中移动到具有加密列的另一组表中（在相同或不同的数据库中）。  
 -  
 -## ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 选项  
 - [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) 和 [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) 都具有 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 选项。 当设置为“开”时（默认为“关”），此选项将取消在大容量复制操作中，在服务器上进行的加密元数据检查，以便用户可以在表或数据库之间大容量复制加密数据，而无需解密数据。  
 -  
 -## 数据迁移方案  
 - 下表显示了适用于多个迁移方案的建议设置。  
 -  
 - ![always-encrypted-migration](../../../relational-databases/security/encryption/media/always-encrypted-migration.PNG "always-encrypted-migration")  
 -  
 -## 加密数据的大容量加载  
 - 使用以下过程加载加密数据。  
 -  
 -1.  对于作为大容量复制操作目标的数据库中的用户，请将该选项设置为“开”。 例如：  
 -  
 -    ```  
 -    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON;  
 -    ```  
 -  
 -2.  Run your bulk copy application or tool connecting as that user. (If your application uses an Always Encrypted enabled client driver, make sure the connection string for the data source does not contain **column encryption setting=enabled** to ensure the data retrieved from encrypted columns remains encrypted. For more information, see [Always Encrypted &#40;client development&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md).)  
 -  
 -3.  Set the ALLOW_ENCRYPTED_VALUE_MODIFICATIONS option back to OFF. For example:  
 -  
 -    ```  
 -    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = OFF;  
 -    ```  
 -  
 -## Potential for Data Corruption  
 - Improper use of this option can lead to data corruption. The **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** option allows the user to insert any data into encrypted columns in the database, including data that is encrypted with different keys, incorrectly encrypted, or not encrypted at all. If the user accidently copies the data that is not correctly encrypted using the encryption scheme (column encryption key, algorithm, encryption type) set up for the target column, you will not be able to decrypt the data (the data will be corrupted). This option must be used carefully, as it can lead to corrupting data in the database.  
 -  
 - The following scenario demonstrates how improperly importing data could lead to data corruption:  
 -  
 -1.  The option is set to ON for a user.  
 -  
 -2.  The user runs the application that connects to the database. The application uses bulk APIs to insert plain text values to encrypted columns. The application expects an Always Encrypted-enabled client driver to encrypt the data on insert. However, the application is misconfigured, so that either it ends up using a driver that does not support Always Encrypted or the connection string does not contain **column encryption setting=enabled**.  
 -  
 -3.  The application sends plaintext values to the server. As cryptographic metadata checks are disabled in the server for the user, the server lets the incorrect data (plaintext instead of correctly encrypted ciphertext) to be inserted into an encrypted column.  
 -  
 -4.  The same or another application connects to the database using an Always Encrypted-enabled driver and with **column encryption setting=enabled** in the connection string, and retrieves the data. The application expects the data to be transparently decrypted. However, the driver fails to decrypt the data because the data is incorrect ciphertext.  
 -  
 -## Best practice  
 -  
 --   Use designated user accounts for long running workloads using this option.  
 -  
 --   For short running bulk copy applications or tools that need to move encrypted data without decrypting it, set the option to ON immediately before running the application and set it back to OFF immediately after running the operation.  
 -  
 --   Do not use this option for developing new applications. Instead, use a client driver (such as  ADO 4.6.1) that offers an API for suppressing cryptographic metadata checks for a single session.  
 -  
 -## See Also  
 - [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)   
 - [ALTER USER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-user-transact-sql.md)   
 - [Always Encrypted &#40;Database Engine&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 - [Always Encrypted Wizard](../../../relational-databases/security/encryption/always-encrypted-wizard.md)   
 - [Always Encrypted &#40;client development&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  

