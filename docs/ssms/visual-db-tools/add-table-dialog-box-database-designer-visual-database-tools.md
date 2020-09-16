---
description: “添加表”对话框（数据库设计器）(Visual Database Tools)
title: “添加表”对话框（数据库设计器）
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65555
- vdt.dlgbox.schema.addtable
ms.assetid: 3c0b1b30-795c-4240-91d6-890b8348014a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 53898206b1111119dad7056e420bf7395d326007
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497304"
---
# <a name="add-table-dialog-box-database-designer-visual-database-tools"></a>“添加表”对话框（数据库设计器）(Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
使用此对话框可以在数据库设计器中添加表。  
  
> [!NOTE]  
> 如果表是为复制发布的，则必须使用 Transact-SQL 语句 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 或 SQL Server 管理对象 (SMO) 对架构进行更改。 使用表设计器或数据库关系图设计器更改架构后，会尝试删除并重新创建表。 由于您不能删除已发布的对象，因此架构更改将失败。  
  
## <a name="ui-element-list"></a>UI 元素列表  
**“刷新”**  
刷新表的列表以与数据库的当前状态匹配。  
  
**添加**  
添加所选的一个或多个表。  
  
> [!NOTE]  
> 如果希望将多个表添加到关系图中，可以将其全部选定，再单击“添加”  。 或者，也可以双击要添加的每个表，然后在完成后单击“关闭”  。  
  
**关闭**  
关闭对话框而不再添加表。  
  
## <a name="see-also"></a>另请参阅  
[向关系图中添加表 (Visual Database Tools)](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
  
