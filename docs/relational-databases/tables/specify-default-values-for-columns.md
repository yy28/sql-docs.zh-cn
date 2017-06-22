---
title: "指定列的默认值 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- columns [SQL Server], defaults
- default values
ms.assetid: 64514aed-b846-407b-992e-cf813f9a1a91
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 956e23e61cb97d5d1adecf4a06f40f734da42948
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="specify-default-values-for-columns"></a>指定列的默认值
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  您可以通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指定将在 [!INCLUDE[tsql](../../includes/tsql-md.md)]的列中输入的默认值。 如果您没有分配默认值，并且将该列保留为空白，则：  
  
-   如果设置了允许空值的选项，则将向该列中插入 NULL。  
  
-   如果没有设置允许空值的选项，则该列将保持空白，但在用户为该列提供值之前，他们将无法保存行。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用以下工具指定默认值：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   如果“默认值”字段中的项替换绑定的默认值（以不带圆括号的形式显示），则将提示你解除对默认值的绑定，并将其替换为新的默认值。  
  
-   若要输入文本字符串，请用单引号 (') 将值括起来；不要使用双引号 (")，因为双引号已保留用于带引号的标识符。  
  
-   若要输入数值默认值，请输入数值并且不要用引号将值括起来。  
  
-   若要输入对象/函数，请输入对象/函数的名称并且不要用引号将名称括起来。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 需要对表的 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-specify-a-default-value-for-a-column"></a>指定列的默认值  
  
1.  在“对象资源管理器”中，右键单击要更改其小数位数的列所在的表，再单击“设计”。  
  
2.  选择要为其指定默认值的列。  
  
3.  在 **“列属性”** 选项卡中，在 **“默认值或绑定”** 属性中输入新的默认值。  
  
    > [!NOTE]  
    >  若要输入数值默认值，请输入该数字。 对于对象或函数，请输入其名称。 对于字母数字默认值，请输入该值，两边用单引号引起来。  
  
4.  在“文件”菜单上，单击“保存”以保存表名。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-specify-a-default-value-for-a-column"></a>指定列的默认值  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    CREATE TABLE dbo.doc_exz ( column_a INT, column_b INT) ;  
    GO  
    INSERT INTO dbo.doc_exz (column_a)VALUES ( 7 ) ;  
    GO  
    ALTER TABLE dbo.doc_exz  
    ADD CONSTRAINT col_b_def  
    DEFAULT 50 FOR column_b ;  
    GO  
  
    ```  
  
 有关详细信息，请参阅 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)。  
  
###  <a name="TsqlExample"></a>  
