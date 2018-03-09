---
title: "“表和列”对话框 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vdt.dlgbox.tablesandcolumns
ms.assetid: 8cf27be1-e66d-4735-a428-9ab4b33af4f5
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0be03d94210fc596bb0902ea130af731b1dadf92
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="tables-and-columns-dialog-box-visual-database-tools"></a>“表和列”对话框 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 使用此对话框可以将一个表中的主键映射到另一个表中的外键。 若要访问此对话框，请在“表设计器”菜单中，单击“关系”。 在“外键关系”对话框中，单击“表和列规范”字段，再单击属性右侧的省略号 **(…)**。  
  
> [!NOTE]  
> 如果表是为复制发布的，则必须使用 Transact-SQL 语句 [ALTER TABLE](http://msdn.microsoft.com/en-us/f1745145-182d-4301-a334-18f799d361d1) 或 SQL Server 管理对象 (SMO) 对架构进行更改。 使用表设计器或数据库关系图设计器更改架构后，会尝试删除并重新创建表。 由于您不能删除已发布的对象，因此架构更改将失败。  
  
## <a name="options"></a>“常规”  
**关系名**  
显示关系的名称。  
  
**主键表**  
列出数据库中的表。 选择将处于关系主键方的表。  
  
**外键表**  
显示处于关系外键方的表。 这是表设计器中的当前所选表。  
  
**主键表下的网格**  
列出在“主键表”列表中选定的表列。 输入分配给该表的主键的列。  
  
**外键表下的网格**  
列出在“外键表”列表中选定的表列。 输入外键表中对应于主键列的外键列。  
  
> [!NOTE]  
> 选作外键的列必须与其对应的主键列具有相同的数据类型。 每个键中列的数目必须相等。 例如，如果关系主键方的表的主键由两列组成，您将需要将这两列中的每一列与关系外键方的表中的列匹配。  
  
## <a name="see-also"></a>另请参阅  
[如何在表之间创建关系 (Visual Database Tools)](http://msdn.microsoft.com/en-us/867a54b8-5be4-46e6-9702-49ae6dabf67c)  
  
