---
title: "复制表 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "复制表"
  - "表 [SQL Server], 复制"
  - "复制表"
  - "表复制 [SQL Server]"
ms.assetid: c6b07423-d1e5-4e5e-8681-5088921f5df3
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# 复制表
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，通过创建新表后从现有表复制列信息，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中复制现有表。  
  
> [!IMPORTANT]  
>  此操作仅复制表的结构，不复制任何表行。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **使用以下工具复制表：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 在目标数据库中要求 CREATE TABLE 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 复制表  
  
1.  请确保您已经连接到要在其中创建表的数据库并在对象资源管理器中选中该数据库。  
  
2.  在对象资源管理器中，右键单击“表”，再单击“新建表”。  
  
3.  在对象资源管理器中，右键单击要复制的表，再单击“设计”。  
  
4.  在现有表中选择列，在 **“编辑”** 菜单上单击 **“复制”**。  
  
5.  切换回新表并选择第一行。  
  
6.  在 **“编辑”** 菜单上，单击 **“粘贴”**。  
  
7.  从“文件”菜单上，单击“保存”表格名称。  
  
8.  在 **“选择名称”** 对话框中，键入新表的名称，然后单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 在查询编辑器中复制表  
  
1.  请确保您已经连接到要在其中创建表的数据库并在对象资源管理器中选中该数据库。  
  
2.  右键单击要复制的表，指向“编写表脚本为”，然后指向“CREATE 到”，再选择“新查询编辑器窗口”。  
  
3.  更改表的名称。  
  
4.  删除新表中不需要的列。  
  
5.  单击“执行” 。  
  
  