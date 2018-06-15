---
title: 修改存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying stored procedures
- editing stored procedures
- stored procedures [SQL Server], modifying
ms.assetid: 13396239-6100-48ce-aa34-461358d99c92
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6f7bdabb6ae916b777f4df6c8965e29a0a4fca63
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32973032"
---
# <a name="modify-a-stored-procedure"></a>修改存储过程
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
    
##  <a name="Top"></a> 本主题介绍了如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中修改存储过程。  
  
-   **准备工作：**[限制和局限](#Restrictions)、[安全性](#Security)  
  
-   **更改过程，使用：**[SQL Server Management Studio](#SSMSProcedure)、[Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程修改为 CLR 存储过程，反之亦然。  
  
 如果原来的过程定义是使用 WITH ENCRYPTION 或 WITH RECOMPILE 创建的，那么只有在 ALTER PROCEDURE 语句中也包含这些选项时，这些选项才有效。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求对过程具有 ALTER PROCEDURE 权限。  
  
##  <a name="Procedures"></a> 修改存储过程  
 您可以使用以下项之一：  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **在 Management Studio 中修改过程**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例，然后展开该实例。  
  
2.  展开 **“数据库”**、过程所属的数据库以及 **“可编程性”**。  
  
3.  展开“存储过程”，右键单击要修改的过程，再单击“修改”。  
  
4.  修改存储过程的文本。  
  
5.  若要测试语法，请在“查询”  菜单上单击“分析” 。  
  
6.  若要将修改信息保存到过程定义中，请在 **“查询”** 菜单上单击 **“执行”**。  
  
7.  若要将更新的过程定义另存为 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本，请在 **“文件”** 菜单上单击 **“另存为”**。 接受该文件名或将其替换为新的名称，再单击 **“保存”**。  
  
> [!IMPORTANT]  
>  验证所有用户的输入。 验证前请勿连接用户输入。 绝对不要执行根据尚未验证的用户输入构造的命令。  
  
###  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **在查询编辑器中修改过程**  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例，然后展开该实例。  
  
2.  展开 **“数据库”**，然后展开过程所属的数据库。 或者，在工具栏上，从可用数据库列表中选择该数据库。 对于此示例，选择 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
3.  在 **“文件”** 菜单上，单击 **“新建查询”**。  
  
4.  复制以下示例并将其粘贴到查询编辑器中。 此示例创建 `uspVendorAllInfo` 过程，该过程返回 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 数据库中所有供应商的名称、所提供的产品、信用等级以及可用性。  
  
    ```  
  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
5.  在 **“文件”** 菜单上，单击 **“新建查询”**。  
  
6.  复制以下示例并将其粘贴到查询编辑器中。 该示例修改 `uspVendorAllInfo` 过程。 将删除 EXECUTE AS CALLER 子句并且将过程的主体修改为只返回那些提供指定产品的供应商。 `LEFT` 和 `CASE` 函数自定义结果集的外观。  
  
    ```  
    ALTER PROCEDURE Purchasing.uspVendorAllInfo  
        @Product varchar(25)   
    AS  
        SET NOCOUNT ON;  
        SELECT LEFT(v.Name, 25) AS Vendor, LEFT(p.Name, 25) AS 'Product name',   
        'Rating' = CASE v.CreditRating   
            WHEN 1 THEN 'Superior'  
            WHEN 2 THEN 'Excellent'  
            WHEN 3 THEN 'Above average'  
            WHEN 4 THEN 'Average'  
            WHEN 5 THEN 'Below average'  
            ELSE 'No rating'  
            END  
        , Availability = CASE v.ActiveFlag  
            WHEN 1 THEN 'Yes'  
            ELSE 'No'  
            END  
        FROM Purchasing.Vendor AS v   
        INNER JOIN Purchasing.ProductVendor AS pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product AS p   
          ON pv.ProductID = p.ProductID   
        WHERE p.Name LIKE @Product  
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
7.  若要将修改信息保存到过程定义中，请在 **“查询”** 菜单上单击 **“执行”**。  
  
8.  若要将更新的过程定义另存为 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本，请在 **“文件”** 菜单上单击 **“另存为”**。 接受该文件名或将其替换为新的名称，再单击 **“保存”**。  
  
9. 若要运行修改的存储过程，请执行以下示例。  
  
    ```  
    EXEC Purchasing.uspVendorAllInfo N'LL Crankarm';  
    GO  
  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER PROCEDURE (Transact-SQL)](../../t-sql/statements/alter-procedure-transact-sql.md)  
  
  
