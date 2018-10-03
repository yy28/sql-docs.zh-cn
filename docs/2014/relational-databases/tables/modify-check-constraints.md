---
title: 修改 CHECK 约束 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, modifying
- modifying constraints
- constraints [SQL Server], check
- constraints [SQL Server], modifying
ms.assetid: f22daef8-e350-40ef-8ff0-b5f87d1d9e56
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aa91f2910fabac44c4c434f70ae3d8bb0ae78c8e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48114037"
---
# <a name="modify-check-constraints"></a>修改 CHECK 约束
  当您希望更改约束表达式或更改对特定条件启用或禁用约束的选项时，可通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中修改 CHECK 约束。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **使用以下工具修改 CHECK 约束：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要对表的 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-a-check-constraint"></a>修改 CHECK 约束  
  
1.  在“对象资源管理器” 中，右键单击包含 CHECK 约束的表，然后选择“设计”。  
  
2.  在 **“表设计器”** 菜单上，单击 **“CHECK 约束…”**。  
  
3.  在 **“CHECK 约束”** 对话框中，在 **“选定的 CHECK 约束”** 下选择要编辑的约束。  
  
4.  完成下表中的相应操作：  
  
    |若要|需要遵循的步骤|  
    |--------|------------------------|  
    |编辑约束表达式|在 **“表达式”** 字段中键入新的表达式。|  
    |重命名约束|在 **“名称”** 字段中键入新的名称。|  
    |将该约束应用于现有数据|选择 **“在创建或启用时检查现有数据”** 选项。|  
    |向表中添加新数据或更新表中现有数据时禁用该约束。|清除 **“对 INSERT 和 UPDATE 强制约束”** 选项。|  
    |当复制代理在表中插入或更新数据时，禁用该约束。|清除 **“强制用于复制”** 选项。|  
  
    > [!NOTE]  
    >  对于 CHECK 约束，有些数据库具有不同的功能。  
  
5.  单击 **“关闭”**。  
  
6.  在“文件”菜单上，单击“保存table name”。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **修改 CHECK 约束**  
  
 必须首先删除现有的 `CHECK` 约束，然后使用新定义重新创建，才能使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]修改 `CHECK` 约束。 有关详细信息，请参阅 [删除 CHECK 约束](delete-check-constraints.md) 和 [创建 CHECK 约束](create-check-constraints.md)。  
  
###  <a name="TsqlExample"></a>  
