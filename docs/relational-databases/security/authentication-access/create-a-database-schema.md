---
title: "创建数据库架构 | Microsoft Docs"
ms.custom: 
ms.date: 07/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.schemas.general.f1
helpviewer_keywords:
- creating schemas with Management Studio
- CREATE SCHEMA [Management Studio]
- database schemas
- schemas [SQL Server], creating
ms.assetid: ed2a5522-f4d2-4111-95a4-d3e1e5081739
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.openlocfilehash: fe8ac92bb4e20d0070cc81e4f58a25babb53a236
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-database-schema"></a>创建数据库架构
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中创建架构。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要创建架构，可使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   新架构由以下数据库级别主体之一拥有：数据库用户、数据库角色或应用程序角色。 在架构内创建的对象由架构所有者拥有，这些对象在 **sys.objects** 中的 **principal_id**为 NULL。 架构所包含对象的所有权可转让给任何数据库级主体，但架构所有者始终保留对该架构内对象的 CONTROL 权限。  
  
-   创建数据库对象时，如果将某一有效的域主体（用户或组）指定为对象所有者，则该域主体将作为架构添加到数据库中。 这个新架构将为该域主体所有。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
  
-   需要对数据库拥有 CREATE SCHEMA 权限。  
  
-   若要指定其他用户作为所创建架构的所有者，则调用方必须具有对该用户的 IMPERSONATE 权限。 如果指定一个数据库角色作为所有者，则调用方必须满足以下任意条件：拥有该角色的成员身份或对该角色的 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
##### <a name="to-create-a-schema"></a>创建架构  
  
1.  在对象资源管理器中，展开 **“数据库”** 文件夹。  
  
2.  展开要在其中创建新数据库架构的数据库。  
  
3.  右键单击“安全性”文件夹，指向“新建”，并选择“架构”。  
  
4.  在“架构 - 新建”对话框中的“常规”页上，在“架构名称”框中输入新架构的名称。  
  
5.  在 **“架构所有者”** 框中，输入要拥有该架构的数据库用户或角色的名称。 或者，单击 **“搜索”** 以打开 **“搜索角色和用户”** 对话框。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>其他选项  
 **“架构– 新建”** 对话框还在两个其他页上提供了选项： **“权限”** 和 **“扩展属性”**。  
  
-   **“权限”** 页将列出所有可能的安全对象以及可授予登录名的针对这些安全对象的权限。  
  
-   **“扩展属性”** 页允许您向数据库用户添加自定义属性。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-schema"></a>创建架构  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  以下示例将创建一个名为 `Chains` 的架构，然后创建名为 `Sizes` 的表。  
    ```sql  
    CREATE SCHEMA Chains;
    GO
    CREATE TABLE Chains.Sizes (ChainID int, width dec(10,2));
    ```

4.  可在单个语句中执行的其他选项。 下面的示例将创建由 Annik 所有、包含表 `NineProngs` 的 `Sprockets` 架构。 该语句向 Mandar 授予 `SELECT` 权限，而对 Prasanna 拒绝授予 `SELECT` 权限。  

    ```sql  
    CREATE SCHEMA Sprockets AUTHORIZATION Annik  
        CREATE TABLE NineProngs (source int, cost int, partnumber int)  
        GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
        DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
    GO  
    ```  
5. 执行以下语句，查看此数据库中的架构：

   ```sql
   SELECT * FROM sys.schemas;
   ```

 有关详细信息，请参阅 [CREATE SCHEMA (Transact-SQL)](../../../t-sql/statements/create-schema-transact-sql.md)。  
  
  
