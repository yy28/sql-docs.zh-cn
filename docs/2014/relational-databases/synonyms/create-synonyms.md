---
title: 创建同义词 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-synonyms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.synonym.general.f1
helpviewer_keywords:
- creating synonyms
- synonyms [SQL Server], creating
ms.assetid: fedfa7a5-d0b6-4e2b-90f4-a08122958e33
caps.latest.revision: 6
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0a0d669a2fdbf1bab9d5b887e7e06d9793bbda9f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014260"
---
# <a name="create-synonyms"></a>创建同义词
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中创建同义词。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **若要创建同义词，可使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
 若要在给定架构中创建同义词，则用户必须具有 CREATE SYNONYM 权限，并拥有架构或具有 ALTER SCHEMA 权限。 CREATE SYNONYM 权限是可授予的权限。  
  
####  <a name="Permissions"></a> Permissions  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-synonym"></a>创建同义词  
  
1.  在 **“对象资源管理器”** 中，展开要创建新视图的数据库。  
  
2.  右键单击“同义词”文件夹，然后单击“新建同义词...”。  
  
3.  在 **“添加同义词”** 对话框中，输入以下信息。  
  
     **同义词名称**  
     键入将用于此对象的新名称。  
  
     **同义词架构**  
     键入将用于此对象的新名称的架构。  
  
     **服务器名称**  
     键入要连接到的服务器实例。  
  
     **数据库名称**  
     键入或选择包含该对象的数据库。  
  
     **架构**  
     键入或选择该对象所属的架构。  
  
     **对象类型**  
     选择对象的类型。  
  
     **对象名称**  
     键入同义词所引用的对象的名称。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-synonym"></a>创建同义词  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 下面的示例为 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中的现有表创建一个同义词。 后续示例中将使用该同义词。  
  
```  
USE tempdb;  
GO  
CREATE SYNONYM MyAddressType  
FOR AdventureWorks2012.Person.AddressType;  
GO  
```  
  
 以下示例将行插入到由 `MyAddressType` 同义词引用的基表。  
  
```  
USE tempdb;  
GO  
INSERT INTO MyAddressType (Name)  
VALUES ('Test');  
GO  
```  
  
 以下示例说明了如何在动态 SQL 中引用同义词。  
  
```  
USE tempdb;  
GO  
EXECUTE ('SELECT Name FROM MyAddressType');  
GO  
```  
  
  