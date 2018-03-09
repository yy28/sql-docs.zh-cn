---
title: "创建数据库主密钥 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c49efaa432cb0a662067b87ef6b6cf32cbeee9b9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="create-a-database-master-key"></a>创建数据库主密钥
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 本主题说明如何使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中创建数据库主密钥。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   [使用 Transact-SQL 创建数据库主密钥](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 要求对数据库具有 CONTROL 权限。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-database-master-key"></a>创建数据库主密钥  
  
1.  选择密码来对存储于该数据库中的主密钥副本进行加密。  
  
2.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
3.  在标准菜单栏上，单击 **“新建查询”**。  
  
4.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- Creates a database master key for the "AdventureWorks2012" database.   
    -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."  
    USE AdventureWorks2012;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
    GO  
    ```  
  
 有关详细信息，请参阅 [CREATE MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-master-key-transact-sql.md)。  
  
  
