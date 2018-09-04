---
title: 教程：所有权链和上下文切换 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.topic: quickstart
applies_to:
- SQL Server 2016
helpviewer_keywords:
- context switching [SQL Server], tutorials
- ownership chains [SQL Server]
ms.assetid: db5d4cc3-5fc5-4cf5-afc1-8d4edc1d512b
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fc70ec0b789ba0873b4e843b77132ec14bf4d7aa
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43024460"
---
# <a name="tutorial-ownership-chains-and-context-switching"></a>Tutorial: Ownership Chains and Context Switching
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
本教程使用一个应用场景说明 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安全性概念，其中包括所有权链和用户上下文切换。  
  
> [!NOTE]  
> 若要在本教程中运行代码，必须已配置混合模式安全性并且已安装 AdventureWorks2017 数据库。 有关混合模式安全性的详细信息，请参阅 [选择身份验证模式](../relational-databases/security/choose-an-authentication-mode.md)。  
  
## <a name="scenario"></a>应用场景  
在此应用场景中，两个用户需要帐户才能访问存储在 AdventureWorks2017 数据库中的采购订单数据。 要求如下：  
  
-   第一个帐户 (TestManagerUser) 必须能够查看每个采购订单中的所有详细信息。  
-   第二个帐户 (TestEmployeeUser) 必须能够根据采购订单号，查看已收到部分货物的项的采购订单号、订单日期、发货日期、产品 ID 号以及每个采购订单中已定购和已收到的项。  
-   所有其他帐户必须保留当前的权限。   
若要满足本应用场景的要求，此示例分为四个部分来说明所有权链和上下文切换的概念：  
  
1.  配置环境。   
2.  创建存储过程以按采购订单访问数据。   
3.  通过存储过程访问数据。  
4.  重置环境。  
  
本示例中的每个代码块都将逐一加以说明。 若要复制完整的示例，请参阅本教程结尾部分的 [完整示例](#CompleteExample) 。

## <a name="prerequisites"></a>必备条件
若要完成本教程，需要 SQL Server Management Studio、针对运行 SQL Server 的服务器的访问权限以及 AdventureWorks 数据库。

- 安装 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安装 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下载 [AdventureWorks2017 示例数据库](https://docs.microsoft.com/sql/samples/adventureworks-install-configure)。

有关在 SQL Server Management Studio 中还原数据库的说明，请参阅[还原数据库](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。   
  
## <a name="1-configure-the-environment"></a>1.配置环境  
使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 及以下代码打开 `AdventureWorks2017` 数据库，然后使用 `CURRENT_USER` [!INCLUDE[tsql](../includes/tsql-md.md)] 语句检查 dbo 用户是否显示为上下文。  
  
```sql
USE AdventureWorks2017;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
```  
  
有关 CURRENT_USER 语句的详细信息，请参阅 [CURRENT_USER (Transact-SQL)](../t-sql/functions/current-user-transact-sql.md)。  
  
使用此代码使 dbo 用户在服务器及 AdventureWorks2017 数据库中创建两个用户。  
  
```sql
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
GO  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
```  
  
有关 CREATE USER 语句的详细信息，请参阅 [CREATE USER (Transact-SQL)](../t-sql/statements/create-user-transact-sql.md)。 有关 CREATE LOGIN 语句的详细信息，请参阅 [CREATE LOGIN (Transact-SQL)](../t-sql/statements/create-login-transact-sql.md)。  
  
使用以下代码将 `Purchasing` 架构的所有权更改为 `TestManagerUser` 帐户。 这样将允许该帐户对其包含的对象使用所有数据操作语言 (DML) 语句访问权限（如 `SELECT` 和 `INSERT` 权限）。 `TestManagerUser` 授予创建存储过程的能力。  
  
```sql
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
```  
  
有关 GRANT 语句的详细信息，请参阅 [GRANT (Transact-SQL)](../t-sql/statements/grant-transact-sql.md)。 有关存储过程的详细信息，请参阅[存储过程（数据库引擎）](../relational-databases/stored-procedures/stored-procedures-database-engine.md)。 有关所有 [!INCLUDE[ssDE](../includes/ssde-md.md)] 权限的海报，请参阅 [https://aka.ms/sql-permissions-poster](https://aka.ms/sql-permissions-poster)。  
  
## <a name="2-create-a-stored-procedure-to-access-data"></a>2.创建存储过程以访问数据  
若要切换数据库内的上下文，请使用 EXECUTE AS 语句。 EXECUTE AS 需要 IMPERSONATE 权限。  
  
使用以下代码中的 `EXECUTE AS` 语句将上下文更改为 `TestManagerUser` ，并创建一个仅显示 `TestEmployeeUser`需要的数据的存储过程。 为了满足这些要求，存储过程接受一个代表采购订单号的变量并且不显示财务信息，WHERE 子句则将结果限制为部分货物。  
  
```sql
EXECUTE AS LOGIN = 'TestManagerUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader a  
      INNER JOIN Purchasing.PurchaseOrderDetail b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END  
GO  
```  
  
当前 `TestEmployeeUser` 对任何数据库对象都没有访问权限。 以下代码（仍位于 `TestManagerUser` 上下文中）授予用户帐户通过存储过程查询基表信息的能力。  
  
```sql
GRANT EXECUTE  
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO  
```  
  
即使没有显式指定架构，存储过程也是 `Purchasing` 架构的一部分，因为默认情况下系统将把 `TestManagerUser` 分配给 `Purchasing` 架构。 您可以使用系统目录信息查找对象，如以下代码所示。  
  
```sql
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas a  
   INNER JOIN sys.objects b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
```  
  
完成本部分示例之后，代码使用 `REVERT` 语句将上下文切换回 dbo。  
  
```sql
REVERT;  
GO  
```  
  
有关 REVERT 语句的详细信息，请参阅 [REVERT (Transact-SQL)](../t-sql/statements/revert-transact-sql.md)。  
  
## <a name="3-access-data-through-the-stored-procedure"></a>3.通过存储过程访问数据  
`TestEmployeeUser` 除了拥有一个登录名以及分配给公共数据库角色的权限之外，对 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库对象没有其他权限。 如果 `TestEmployeeUser` 试图访问基表，以下代码在将返回一个错误。  
  
```sql
EXECUTE AS LOGIN = 'TestEmployeeUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* This won't work */  
SELECT *  
FROM Purchasing.PurchaseOrderHeader;  
GO  
SELECT *  
FROM Purchasing.PurchaseOrderDetail;  
GO  
```  

返回的错误：
```
Msg 229, Level 14, State 5, Line 6
The SELECT permission was denied on the object 'PurchaseOrderHeader', database 'AdventureWorks2017', schema 'Purchasing'.
```
  
因为在最后一部分中创建的存储过程引用的对象由 `TestManagerUser` 凭借 `Purchasing` 架构所有权而拥有，因此 `TestEmployeeUser` 可以通过此存储过程访问基表。 以下代码仍使用 `TestEmployeeUser` 上下文将采购订单 952 作为参数传递。  
  
```sql
EXEC Purchasing.usp_ShowWaitingItems 952  
GO  
```  
  
## <a name="4-reset-the-environment"></a>4.重置环境  
以下代码使用 `REVERT` 命令将当前帐户的上下文返回至 `dbo`，然后重置环境。  
  
```sql
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="CompleteExample"></a>完整示例  
本部分显示完整的示例代码。  
  
> [!NOTE]  
> 此代码不包括两个说明 `TestEmployeeUser` 无法从基表中进行选择的预期错误。  
  
```sql
/*   
Script:       UserContextTutorial.sql  
Author:       Microsoft  
Last Updated: Books Online  
Conditions:   Execute as DBO or sysadmin in the AdventureWorks database  
Section 1:    Configure the Environment   
*/  
USE AdventureWorks2017;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* Create server and database users */  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
  
GO  
  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
  
/*   
Section 2: Switch Context and Create Objects  
*/  
EXECUTE AS LOGIN = 'TestManagerUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader AS a  
      INNER JOIN Purchasing.PurchaseOrderDetail AS b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END;  
GO  
  
/* Give the employee the ability to run the procedure */  
GRANT EXECUTE   
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO   
  
/* Notice that the stored procedure is located in the Purchasing   
schema. This also demonstrates system catalogs */  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas AS a  
   INNER JOIN sys.objects AS b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
  
/* Go back to being the dbo user */  
REVERT;  
GO  
  
/*  
Section 3: Switch Context and Observe Security   
*/  
EXECUTE AS LOGIN = 'TestEmployeeUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
EXEC Purchasing.usp_ShowWaitingItems 952;  
GO  
  
/*   
Section 4: Clean Up Example  
*/  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
[SQL Server 数据库引擎和 Azure SQL Database 的安全中心](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
  
