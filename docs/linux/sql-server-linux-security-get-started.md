---
title: Linux 上的 SQL Server 安全入门 |Microsoft Docs
description: 本指南介绍了典型的安全操作。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.custom: sql-linux
ms.openlocfilehash: c3d3c4a6ac5d5d49e880fc2af1546bdcf9a73779
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211736"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Linux 上的 SQL Server 的安全功能演练

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

如果你是刚接触 SQL Server 的 Linux 用户，以下任务将指导你完成某些安全任务。 虽然这些并非 Linux 独有或特定的任务，但能有助于你了解需要深入了解的领域。 在每个示例中，均提供该领域的详细文档链接。

> [!NOTE]
>  下面的示例使用**AdventureWorks2014**示例数据库。 有关如何获取和安装此示例数据库的说明，请参阅[SQL Server 数据库从 Windows 还原到 Linux](sql-server-linux-migrate-restore-database.md)。


## <a name="create-a-login-and-a-database-user"></a>创建登录名和数据库用户 

通过使用在 master 数据库中创建的登录名授予其他人访问 SQL Server [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)语句。 例如：

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

> [!NOTE]
>  在前一命令中始终使用强密码代替星号。

登录名可连接到 SQL Server，且能（通过有限权限）访问 master 数据库。 若要连接到用户数据库，登录名需要数据库级别的相应标识，称为数据库用户。 用户特定于每个数据库，且必须在每个要向其授予访问权限的数据库中单独创建。 下面的示例移至 AdventureWorks2014 数据库，然后使用[CREATE USER](../t-sql/statements/create-user-transact-sql.md)语句以创建名为 Larry 的是与名为 Larry 的登录名相关联的用户。 尽管该登录名和用户相关（相互映射），但它们是不同的对象。 登录名是服务器级主体。 用户是数据库级主体。

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- SQL Server 管理员帐户可连接到任何数据库，并可在任何数据库中创建更多登录名和用户。  
- 当用户创建数据库时，他们会成为数据库所有者，可连接到该数据库。 数据库所有者可以创建更多用户。

更高版本可以授权其他登录名创建更多的登录名通过向它们授予`ALTER ANY LOGIN`权限。 在数据库中，可以授权其他用户创建更多用户通过向它们授予`ALTER ANY USER`权限。 例如：   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

现在 Larry 的登录名，可以创建更多登录名和用户 Jerry 可以创建更多的用户。


## <a name="granting-access-with-least-privileges"></a>授予特权最少的访问权限

第一个连接到用户数据库的用户将是管理员和数据库所有者帐户。 但是这些用户在数据库上具有提供的所有权限。 其权限要比大多数用户应该拥有的更多。 

如果你刚开始，可以使用内置的分配某些常规类别的权限*固定数据库角色的成员*。 例如，`db_datareader`固定的数据库角色可以读取所有表在数据库中，但不进行任何更改。 通过使用授予固定的数据库角色的成员身份[ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md)语句。 下面的示例将用户添加`Jerry`到`db_datareader`固定的数据库角色。   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

固定的数据库角色的列表，请参阅[数据库级别角色](../relational-databases/security/authentication-access/database-level-roles.md)。

更高版本，若要配置更精确的访问权限 （强烈建议） 在数据准备就绪后，创建你自己使用的用户定义的数据库角色[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)语句。 然后将特定精细权限分配给自定义角色。

例如，以下语句创建名为的数据库角色`Sales`，授予`Sales`组的功能，请参阅、 更新和删除行`Orders`表，然后将用户添加`Jerry`到`Sales`角色。   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```   

For more information about the permission system, see [Getting Started with Database Engine Permissions](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).


## Configure row-level security  

[Row-Level Security](../relational-databases/security/row-level-security.md) enables you to restrict access to rows in a database based on the user executing a query. This feature is useful for scenarios like ensuring that customers can only access their own data or that workers can only access data that is pertinent to their department.   

The following steps walk through setting up two Users with different row-level access to the `Sales.SalesOrderHeader` table. 

Create two user accounts to test the row level security:    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

Grant read access on the `Sales.SalesOrderHeader` table to both users:    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
Create a new schema and inline table-valued function. The function returns 1 when a row in the `SalesPersonID` column matches the ID of a `SalesPerson` login or if the user executing the query is the Manager user.   
   
```     
CREATE SCHEMA Security;   
GO   
   
CREATE FUNCTION Security.fn_securitypredicate(@SalesPersonID AS int)     
    RETURNS TABLE   
WITH SCHEMABINDING   
AS     
   RETURN SELECT 1 AS fn_securitypredicate_result    
WHERE ('SalesPerson' + CAST(@SalesPersonId as VARCHAR(16)) = USER_NAME())     
    OR (USER_NAME() = 'Manager');    
```   

Create a security policy adding the function as both a filter and a block predicate on the table:  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

Execute the following to query the `SalesOrderHeader` table as each user. Verify that `SalesPerson280` only sees the 95 rows from their own sales and that the `Manager` can see all the rows in the table.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
Alter the security policy to disable the policy.  Now both users can access all rows. 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## Enable dynamic data masking

[Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md) enables you to limit the exposure of sensitive data to users of an application by fully or partially masking certain columns. 

Use an `ALTER TABLE` statement to add a masking function to the `EmailAddress` column in the `Person.EmailAddress` table: 
 
```
使用 AdventureWorks2014;转 ALTER 表 Person.EmailAddress     ALTER 列电子邮件地址    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
Create a new user `TestUser` with `SELECT` permission on the table, then execute a query as `TestUser` to view the masked data:   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
Verify that the masking function changes the email address in the first record from:
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## Enable Transparent Data Encryption

One threat to your database is the risk that someone will steal the database files off of your hard-drive. This could happen with an intrusion that gets elevated access to your system, through the actions of a problem employee, or by theft of the computer containing the files (such as a laptop).

Transparent Data Encryption (TDE) encrypts the data files as they are stored on the hard drive. The master database of the SQL Server database engine has the encryption key, so that the database engine can manipulate the data. The database files cannot be read without access to the key. High-level administrators can manage, backup, and recreate the key, so the database can be moved, but only by selected people. When TDE is configured, the `tempdb` database is also automatically encrypted. 

Since the Database Engine can read the data, Transparent Data Encryption does not protect against unauthorized access by administrators of the computer who can directly read memory, or access SQL Server through an administrator account.

### Configure TDE

- Create a master key
- Create or obtain a certificate protected by the master key
- Create a database encryption key and protect it by the certificate
- Set the database to use encryption

Configuring TDE requires `CONTROL` permission on the master database and `CONTROL` permission on the user database. Typically an administrator configures TDE. 

The following example illustrates encrypting and decrypting the `AdventureWorks2014` database using a certificate installed on the server named `MyServerCert`.


```
USE master;  
前往  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
前往  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
前往  

使用 AdventureWorks2014; 转
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
前往
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON；   
```

To remove TDE, execute `ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

The encryption and decryption operations are scheduled on background threads by SQL Server. You can view the status of these operations using the catalog views and dynamic management views in the list that appears later in this topic.   

> [!WARNING]
>  Backup files of databases that have TDE enabled are also encrypted by using the database encryption key. As a result, when you restore these backups, the certificate protecting the database encryption key must be available. This means that in addition to backing up the database, you have to make sure that you maintain backups of the server certificates to prevent data loss. Data loss will result if the certificate is no longer available. For more information, see [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  

For more information about TDE, see [Transparent Data Encryption (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md).   


## Configure backup encryption
SQL Server has the ability to encrypt the data while creating a backup. By specifying the encryption algorithm and the encryptor (a certificate or asymmetric key) when creating a backup, you can create an encrypted backup file.    
  
> [!WARNING]  
>  It is very important to back up the certificate or asymmetric key, and preferably to a different location than the backup file it was used to encrypt. Without the certificate or asymmetric key, you cannot restore the backup, rendering the backup file unusable. 
 
 
The following example creates a certificate, and then creates a backup protected by the certificate.
```
使用 master; 转 创建证书 BackupEncryptCert   SUBJECT = 数据库备份; 转到备份数据库 [AdventureWorks2014] 到磁盘 = N'/var/opt/mssql/backups/AdventureWorks2014.bak  
替换为  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ），  
  STATS = 10  
前往  
```

For more information, see [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md).


## Next steps

For more information about the security features of SQL Server, see [Security Center for SQL Server Database Engine and Azure SQL Database](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).
