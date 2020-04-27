---
title: 增加数据库的大小 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], size
- increasing database size
- database size [SQL Server], increasing
- size [SQL Server], databases
ms.assetid: 14f4206d-3afa-4ba9-9849-23e81d63306d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 02a34ba1e0f441b665c239d60f6398afa4247102
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62917231"
---
# <a name="increase-the-size-of-a-database"></a>增加数据库的大小
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中增加数据库的大小。 通过增加现有数据或日志文件的大小或向数据库添加新文件，可以扩展数据库。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **增加数据库的大小，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   当 BACKUP 语句正在运行时，不能添加或删除文件。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 需要对数据库拥有 ALTER 权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-increase-the-size-of-a-database"></a>增加数据库的大小  
  
1.  在 **对象资源管理器**中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例，然后展开该实例。  
  
2.  展开  “数据库”，右键单击要扩展的数据库，再单击  “属性”。  
  
3.  在 **“数据库属性”** 中，选择 **“文件”** 页。  
  
4.  若要增加现有文件的大小，请增加文件的  “初始大小 (MB)”列中的值。 数据库的大小必须至少增加 1 MB。  
  
5.  若要通过添加新文件增加数据库大小，请单击 **“添加”** ，然后输入新文件的值。 有关详细信息，请参阅 [向数据库中添加数据文件或日志文件](add-data-or-log-files-to-a-database.md)。  
  
6.  单击“确定”。   
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-increase-the-size-of-a-database"></a>增加数据库的大小  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。 此示例可增加文件 `test1dat3`的大小。  
  
 [!code-sql[DatabaseDDL#AlterDatabase5](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase5)]  
  
 有关更多示例，请参阅 [ALTER DATABASE 文件和文件组选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)。  
  
## <a name="see-also"></a>另请参阅  
 [向数据库中添加数据文件或日志文件](add-data-or-log-files-to-a-database.md)   
 [收缩数据库](shrink-a-database.md)  
  
  
