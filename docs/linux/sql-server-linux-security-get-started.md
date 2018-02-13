---
title: "在 Linux 上的 SQL Server 安全入门 |Microsoft 文档"
description: "本指南介绍了典型的安全操作。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.technology: database-engine
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.custom: sql-linux
ms.workload: Inactive
ms.openlocfilehash: 00c222c601cdf314f04db3cb9e3b818d9ea3a65f
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2018
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Linux 上的 SQL Server 的安全功能演练

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

如果你不熟悉 SQL Server 的 Linux 用户，以下任务将指导你完成一些安全任务。 虽然这些并非 Linux 独有或特定的任务，但能有助于你了解需要深入了解的领域。 在每个示例中，均提供该领域的详细文档链接。

>  [!NOTE]
>  下面的示例使用**AdventureWorks2014**示例数据库。 有关如何获取和安装此示例数据库的说明，请参阅[从 Windows 的 SQL Server 数据库还原到 Linux](sql-server-linux-migrate-restore-database.md)。


## <a name="create-a-login-and-a-database-user"></a>创建登录名和数据库用户 

通过在 master 数据库中使用创建登录名授予其他人访问 SQL Server [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)语句。 例如：

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

>  [!NOTE]
>  始终在前一个命令中使用强密码来代替星号。

登录名可连接到 SQL Server，且能（通过有限权限）访问 master 数据库。 若要连接到用户数据库，登录名需要数据库级别的相应标识，称为数据库用户。 用户特定于每个数据库，且必须在每个要向其授予访问权限的数据库中单独创建。 下面的示例到 AdventureWorks2014 数据库中，可使您移动，然后使用[CREATE USER](../t-sql/statements/create-user-transact-sql.md)语句以创建名为 Larry 都与名为 Larry 的登录名相关联的用户。 尽管该登录名和用户相关（相互映射），但它们是不同的对象。 登录名是服务器级主体。 用户是数据库级主体。

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- SQL Server 管理员帐户可连接到任何数据库，并可在任何数据库中创建更多登录名和用户。  
- 当用户创建数据库时，他们会成为数据库所有者，可连接到该数据库。 数据库所有者可以创建更多用户。

更高版本可以授权其他登录名创建多个登录名授予他们`ALTER ANY LOGIN`权限。 数据库中可以授权其他用户创建更多用户通过向他们授予`ALTER ANY USER`权限。 例如：   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

现在，登录名 Jerry 可以创建更多登录名，用户 Jerry 可以创建更多用户。


## <a name="granting-access-with-least-privileges"></a>授予特权最少的访问权限

第一个连接到用户数据库的用户将是管理员和数据库所有者帐户。 但这些用户具有数据库的所有权限。 其权限要比大多数用户应该拥有的更多。 

你刚开始时，你可以通过使用内置分配权限的一些常规类别*固定数据库角色的成员*。 例如，`db_datareader`固定的数据库角色可以读取所有表在数据库中，但不执行更改。 通过使用授予固定的数据库角色的成员身份[ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md)语句。 下面的示例将用户添加`Jerry`到`db_datareader`固定的数据库角色。   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

固定的数据库角色的列表，请参阅[数据库级角色](../relational-databases/security/authentication-access/database-level-roles.md)。

更高版本，当你准备好配置更精确地访问数据 （强烈建议），创建您自己使用的用户定义的数据库角色[创建角色](../t-sql/statements/create-role-transact-sql.md)语句。 然后将特定精细权限分配给自定义角色。

例如，以下语句创建名为的数据库角色`Sales`，授予`Sales`组能够查看、 更新和删除行`Orders`表，并将用户`Jerry`到`Sales`角色。   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```   

有关权限系统的详细信息，请参阅[Getting Started with Database Engine Permissions](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。


## <a name="configure-row-level-security"></a>配置行级安全性  

[行级别安全性](../relational-databases/security/row-level-security.md)使您能够将访问限制为基于执行查询的用户数据库中的行。 在某些情况下（如确保客户只能访问自己的数据，或员工只能访问与其部门相关的数据）此功能很有用。   

以下步骤引导设置两个具有不同的行级访问权限的用户`Sales.SalesOrderHeader`表。 

创建两个用户帐户，测试行级安全性：    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

在上授予读取访问权限`Sales.SalesOrderHeader`表添加到这两个用户：    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
创建新架构和内联表值函数。 该函数将返回 1 中的行时`SalesPersonID`列匹配的 ID`SalesPerson`登录名或执行查询的用户是否是 Manager 用户。   
   
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

创建一个安全策略，将函数添加为表上的筛选器和阻止谓词：  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

执行以下查询`SalesOrderHeader`表为每个用户。 验证`SalesPerson280`只看到从他们自己的销售和，95 行`Manager`可以看到表中的所有行。  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
更改安全策略以禁用策略。  现在，这两位用户均可访问所有行。 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## <a name="enable-dynamic-data-masking"></a>启用动态数据掩码

[动态数据屏蔽](../relational-databases/security/dynamic-data-masking.md)使您能够限制敏感数据的公开应用程序的用户的完全或部分屏蔽某些列。 

使用`ALTER TABLE`语句来添加到了屏蔽函数`EmailAddress`中的列`Person.EmailAddress`表： 
 
```
USE AdventureWorks2014;
GO
ALTER TABLE Person.EmailAddress    
ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
创建一个新用户`TestUser`与`SELECT`权限表中，然后执行为查询`TestUser`查看经过屏蔽的数据：   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
验证掩码函数是否更改来自以下地址的第一记录中的电子邮件地址：
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## <a name="enable-transparent-data-encryption"></a>启用透明数据加密

数据库面临的一种威胁是有人可能会窃取硬盘中的数据库文件。 因不良员工行为不轨，或者某人偷走包含文件的计算机（如笔记本电脑），然后提升访问权限入侵系统，这时可能会发生这种情况。

透明数据加密 (TDE) 在数据文件存储在硬盘驱动器上时会对其加密。 SQL Server 数据库引擎的 master 数据库具有加密密钥，因此数据库引擎可以处理数据。 没有密钥访问权限就不能读取数据库文件。 高级管理员可以管理、备份和重新创建密钥，因此可以移动数据库（但仅能由所选人员操作）。 当配置 TDE 时，`tempdb`数据库也自动加密。 

由于数据库引擎可以读取数据，透明数据加密不能防止可以直接读取内存或者可以通过管理员帐户访问 SQL Server 的计算机管理员执行未经授权的访问。

### <a name="configure-tde"></a>配置 TDE

- 创建主密钥
- 创建或获取由主密钥保护的证书
- 创建数据库加密密钥并通过此证书保护该密钥
- 将数据库设置为使用加密

配置 TDE 需要`CONTROL`的主数据库上的权限和`CONTROL`对用户数据库的权限。 通常，由管理员配置 TDE。 

下面的示例演示如何使用安装在名为 `AdventureWorks2014` 的服务器上的证书加密和解密 `MyServerCert`数据库。


```
USE master;  
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
GO  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
GO  

USE AdventureWorks2014;  
GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON;   
```

若要删除 TDE，执行 `ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

加密和解密操作由 SQL Server 安排在后台线程中执行。 您可以使用本主题后面部分显示的列表中的目录视图和动态管理视图查看这些操作的状态。   

>  [!WARNING]
>  启用了 TDE 的数据库的备份文件也使用数据库加密密钥进行加密。 因此，当您还原这些备份时，用于保护数据库加密密钥的证书必须可用。 也就是说，除了备份数据库之外，您还要确保自己保留了服务器证书的备份以防数据丢失。 如果证书不再可用，将会导致数据丢失。 有关详细信息，请参阅 [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)。  

有关 TDE 的详细信息，请参阅[透明数据加密 (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md)。   


## <a name="configure-backup-encryption"></a>配置备份加密
SQL Server 可在创建备份时加密数据。 通过在创建备份时指定加密算法和加密程序（证书或非对称密钥），可创建加密的备份文件。    
  
> [!WARNING]  
>  备份证书或非对称密钥很重要，并且备份的位置最好与其用于加密的备份文件不同。 没有证书或非对称密钥，即无法还原备份，从而使备份文件无法重用。 
 
 
以下示例创建一个证书，然后创建受此证书保护的备份。
```
USE master;  
GO  
CREATE CERTIFICATE BackupEncryptCert   
   WITH SUBJECT = 'Database backups';  
GO 
BACKUP DATABASE [AdventureWorks2014]  
TO DISK = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
```

有关详细信息，请参阅[备份加密](../relational-databases/backup-restore/backup-encryption.md)。


## <a name="next-steps"></a>后续步骤

SQL server 的安全功能的详细信息，请参阅[SQL Server 数据库引擎和 Azure SQL 数据库安全中心](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。
