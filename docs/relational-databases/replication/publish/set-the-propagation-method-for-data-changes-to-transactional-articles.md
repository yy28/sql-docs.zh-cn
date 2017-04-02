---
title: "为事务项目的数据更改设置传播方法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "事务复制, 传播方法"
  - "传播数据更改 [SQL Server 复制]"
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 为事务项目的数据更改设置传播方法
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中为事务项目的数据更改设置传播方法。  
  
 默认情况下，事务复制使用一组存储过程将每个项目的更改传播到订阅服务器。 可以使用自定义过程替换这些存储过程。 有关详细信息，请参阅 [指定如何为事务项目传播更改](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
-   **为事务项目的数据更改设置传播方法，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   在编辑复制生成的任何快照文件时，都必须谨慎。 必须测试和支持自定义存储过程中的自定义逻辑。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 不支持自定义逻辑。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 上，指定传播方法 **属性** 的选项卡上 **项目属性-\< 项目>** 对话框中，可以在新建发布向导和 **发布属性-\< 发布>** 对话框。 有关使用向导和访问对话框中的详细信息，请参阅 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md) 和 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 指定传播方法  
  
1.  在 **文章** 新建发布向导的页面或 **发布属性-\< 发布>** 对话框中，选择一个表，然后单击 **项目属性**。  
  
2.  单击 **“设置突出显示的表项目的属性”**。  
  
3.  在 **属性** 的选项卡上 **项目属性-\< 项目>** 对话框中，在 **语句传递** 部分中，指定传播方法为每个操作使用 **INSERT 传递格式**, ，**UPDATE 传递格式**, ，和 **DELETE 传递格式** 菜单。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您在 **发布属性-\< 发布>** 对话框中，单击 **确定** 以保存并关闭对话框。  
  
#### 生成和使用自定义存储过程  
  
1.  在 **文章** 新建发布向导的页面或 **发布属性-\< 发布>** 对话框中，选择一个表，然后单击 **项目属性**。  
  
2.  单击 **“设置突出显示的表项目的属性”**。  
  
     上 **属性** 的选项卡上 **项目属性-\< 项目>** 对话框中，在 **语句传递** 部分中，从适当传递格式菜单中选择 CALL 语法 (**INSERT 传递格式**, ，**UPDATE 传递格式**, ，或 **DELETE 传递格式**)，然后键入要在中使用的过程的名称 **INSERT 存储过程**, ，**DELETE 存储过程**, ，或 **更新存储过程**。 有关 CALL 语法的详细信息，请参阅"存储过程的 Call 语法"一节中 [指定如何为事务项目传播更改](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  如果您在 **发布属性-\< 发布>** 对话框中，单击 **确定** 以保存并关闭对话框。  
  
5.  发布的快照生成后，将包含上一步骤中指定的过程。 这些过程将使用指定的 CALL 语法，但将包含复制使用的默认逻辑。  
  
     快照生成后，定位到此项目所属的发布的快照文件夹，并找到与此项目同名的 **.sch** 文件。 使用记事本或其他文本编辑器打开此文件，找到用于插入、更新或删除存储过程的 CREATE PROCEDURE 命令，并编辑过程定义，以为传播数据更改提供自定义逻辑。 重新生成快照后，必须重新创建自定义过程。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 通过事务复制，您可以控制如何将更改从发布服务器传播到订阅服务器，而这种传播方法可以在创建和之后更改项目时使用复制存储过程以编程的方式进行设置。  
  
> [!NOTE]  
>  可以为作用于发布数据行的每一种 DML（数据操作语言）操作（插入、更新或删除）指定一种不同的传播方法。  
  
 有关详细信息，请参阅 [指定如何为事务项目传播更改](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
#### 创建使用 Transact-SQL 命令传播数据更改的项目  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定项目所属的发布名称 **@publication**, ，项目的名称，为 **@article**, 要发布的数据库对象 **@source_object**, ，且值为 **SQL** 为至少一个以下参数︰  
  
    -   **@ins_cmd** -控制复制 [插入](../../../t-sql/statements/insert-transact-sql.md) 命令。  
  
    -   **@upd_cmd** -控制复制 [更新](../../../t-sql/queries/update-transact-sql.md) 命令。  
  
    -   **@del_cmd** -控制复制 [删除](../../../t-sql/statements/delete-transact-sql.md) 命令。  
  
    > [!NOTE]  
    >  指定的值时 **SQL** 对于任何上述参数，该类型的命令将复制到订阅服务器上作为相应 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 命令。  
  
     有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
#### 创建不传播数据更改的项目  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定项目所属的发布名称 **@publication**, ，项目的名称，为 **@article**, 要发布的数据库对象 **@source_object**, ，且值为 **NONE** 为至少一个以下参数︰  
  
    -   **@ins_cmd** -控制复制 [插入](../../../t-sql/statements/insert-transact-sql.md) 命令。  
  
    -   **@upd_cmd** -控制复制 [更新](../../../t-sql/queries/update-transact-sql.md) 命令。  
  
    -   **@del_cmd** -控制复制 [删除](../../../t-sql/statements/delete-transact-sql.md) 命令。  
  
    > [!NOTE]  
    >  指定的值时 **NONE** 对于任何上述参数，该类型的命令不会复制到订阅服务器。  
  
     有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
#### 通过用户修改的自定义存储过程创建项目  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定项目所属的发布名称 **@publication**, ，项目的名称，为 **@article**, 要发布的数据库对象 **@source_object**, 的值 **@schema_option** 包含的值的位掩码 **0x02** （使自动生成自定义存储过程），以及至少一个以下参数︰  
  
    -   **@ins_cmd** -将值指定为 **CALL sp_MSins_*article_name***, ，其中 ***article_name*** 为指定的值 **@article**。  
  
    -   **@del_cmd** -将值指定为 **调用 sp_MSdel_*article_name*** 或 **XCALL sp_MSdel_*article_name***, ，其中 ***article_name*** 为指定的值 **@article**。  
  
    -   **@upd_cmd** -将值指定为 **SCALL sp_MSupd_*article_name***, ，**调用 sp_MSupd_*article_name***, ，**XCALL sp_MSupd_*article_name***, ，或 **MCALL sp_MSupd_*article_name***, ，其中 ***article_name*** 为指定的值 **@article**。  
  
    > [!NOTE]  
    >  对于以上每个命令参数，您都可以为复制生成的存储过程指定您自己的名称。  
  
    > [!NOTE]  
    >  调用、 SCALL、 XCALL 和 MCALL 语法的详细信息，请参阅 [指定如何为事务项目传播更改](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
     有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  快照生成后，定位到此项目所属的发布的快照文件夹，并找到与此项目同名的 **.sch** 文件。 使用 Notepad.exe 打开此文件，找到用于插入、更新或删除存储过程的 CREATE PROCEDURE 命令，并编辑过程定义以提供用于传播数据更改的任何自定义逻辑。 有关详细信息，请参阅 [指定如何为事务项目传播更改](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
#### 用自定义存储过程中的自定义脚本创建项目以传播数据更改  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定项目所属的发布名称 **@publication**, ，项目的名称，为 **@article**, 要发布的数据库对象 **@source_object**, 的值 **@schema_option** 包含的值的位掩码 **0x02** （使自动生成自定义存储过程），以及至少一个以下参数︰  
  
    -   **@ins_cmd** -将值指定为 **CALL sp_MSins_*article_name***, ，其中 ***article_name*** 为指定的值 **@article**。  
  
    -   **@del_cmd** -将值指定为 **调用 sp_MSdel_*article_name*** 或 **XCALL sp_MSdel_*article_name***, ，其中 ***article_name*** 为指定的值 **@article**。  
  
    -   **@upd_cmd** -将值指定为 **SCALL sp_MSupd_*article_name***, ，**调用 sp_MSupd_*article_name***, ，**XCALL sp_MSupd_*article_name***, ，**MCALL sp_MSupd_*article_name***, ，其中 ***article_name*** 为指定的值 **@article**。  
  
    > [!NOTE]  
    >  对于以上每个命令参数，您都可以为复制生成的存储过程指定您自己的名称。  
  
    > [!NOTE]  
    >  调用、 SCALL、 XCALL 和 MCALL 语法的详细信息，请参阅 [指定如何为事务项目传播更改](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
     有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在发布服务器上对发布数据库中，使用 [ALTER PROCEDURE](../../../t-sql/statements/alter-procedure-transact-sql.md) 语句来编辑 [sp_scriptpublicationcustomprocs](../../../relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql.md) ，以便它返回 [CREATE PROCEDURE](../../../t-sql/statements/create-procedure-transact-sql.md) 来执行插入、 更新和删除自定义存储过程的脚本。 有关详细信息，请参阅 [指定如何为事务项目传播更改](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
#### 更改为现有项目传播更改的方法  
  
1.  在发布服务器上对发布数据库中，执行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)。 指定 **@publication**, ，**@article**, ，值为 **ins_cmd**, ，**upd_cmd**, ，或 **del_cmd** 为 **@property**, ，和适当的传播方法 **@value**。  
  
2.  为每个要更改的传播方法重复步骤 1。  
  
## 另请参阅  
 [指定如何传播事务项目的更改](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)   
 [创建、 修改和删除发布和文章和 #40;复制和 #41;](../../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md)  
  
  