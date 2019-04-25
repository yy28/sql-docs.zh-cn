---
title: 对复制禁用外键约束 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- constraints [SQL Server], foreign keys
- foreign keys [SQL Server], disabling constraints
- disabling constraints
ms.assetid: 4211f2fd-d16a-4081-995c-43f1f0827f0b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2cd2e4f3e5ee16c02ba48c6cd8ced98c06133dfb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62761070"
---
# <a name="disable-foreign-key-constraints-for-replication"></a>对复制禁用外键约束
  可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中对复制禁用外键约束。 如果正在从以前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布数据，这很有用。  
  
> [!NOTE]  
>  如果表是使用复制发布的，则对于复制代理执行的操作将自动禁用外键约束。 当复制代理在订阅服务器上执行插入、更新或删除操作时，将不检查约束；如果用户执行插入、更新或删除操作，则检查约束。 由于最初插入、更新或删除数据时已经在发布服务器上检查过约束，所以对于复制代理将禁用该约束。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **对复制禁用外键约束，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要对表的 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>对复制禁用外键约束  
  
1.  在 **“对象资源管理器”** 中，展开具有要修改的外键约束的表，再展开 **“键”** 文件夹。  
  
2.  右键单击外键约束，再单击“修改”。  
  
3.  在 **“外键关系”** 对话框，针对 **“强制用于复制”** 选择 **“否”** 值。  
  
4.  单击 **“关闭”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>对复制禁用外键约束  
  
1.  若要在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中执行此任务，请删除外键约束。 然后添加一个新外键约束，并指定 NOT FOR REPLICATION 选项。  
  
 有关详细信息，请参阅 [ALTER TABLE (Transact-SQL)](/sql/t-sql/statements/alter-table-transact-sql)。  
  
###  <a name="TsqlExample"></a>  
