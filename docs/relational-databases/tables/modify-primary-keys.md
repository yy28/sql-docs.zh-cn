---
title: "修改主键 | Microsoft Docs"
ms.custom: 
ms.date: 07/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying primary keys
- primary keys [SQL Server], modifying
ms.assetid: 8e2a15ba-1cd1-4408-b860-16c3ee37d635
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: becb37a9eb7767299706bd354e7801a255b0dc96
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="modify-primary-keys"></a>修改主键
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  您可以通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 修改 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的主键。 您可以通过更改列顺序、索引名称、聚集选项或填充因子，修改表的主键。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **使用以下工具修改主键：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要对表的 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-a-primary-key"></a>修改主键  
  
1.  打开要修改其主键的表的表设计器，在此表设计器中单击右键，然后从快捷菜单中选择“索引/键”。  
  
2.  在“索引/键”对话框中，从“选定的主/唯一键或索引”列表中选择主键索引。  
  
3.  完成下表中的相应操作：  
  
    |若要|需要遵循的步骤|  
    |--------|------------------------|  
    |重命名主键|在 **“名称”** 框中键入新名称。 确保新名称不与“选定的主/唯一键或索引”列表中的名称重复。|  
    |设置聚集选项|若要为主键创建聚集索引，请选择“创建为聚集的”，再从下拉列表框中选择相应的选项。 对于每个表，只允许存在一个聚集索引。 如果此选项对您的索引不可用，则您必须首先对现有的聚集索引清除此设置。<br /><br /> 如果未选择此选项，则创建唯一的非聚集索引。|  
    |定义填充因子|展开 **“填充规范”** 类别，然后在 **“填充因子”** 框中键入一个 0 到 100 之间的整数。 有关填充因子及其用途的详细信息，请参阅 [为索引指定填充因子](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)。|  
    |更改列顺序|选择“列”，再单击属性右侧的省略号 (…)。 在  **“索引列”** 对话框中，将这些列从主键中删除。 然后，按所需顺序重新添加这些列。 若要将某列从键中移除，只需将其列名从 **“列”** 名称列表名称中移除即可。|  
  
4.  在“文件”菜单上，单击“保存table name”。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **修改主键**  
  
 若要使用 Transact-SQL 修改 PRIMARY KEY 约束，必须先删除现有的 PRIMARY KEY 约束，然后再用新定义重新创建该约束。 有关详细信息，请参阅 [Delete Primary Keys](../../relational-databases/tables/delete-primary-keys.md) 和 [Create Primary Keys](../../relational-databases/tables/create-primary-keys.md)。  
  
###  <a name="TsqlExample"></a>  
