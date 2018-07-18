---
title: “添加表”对话框（数据库设计器）(Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65555
- vdt.dlgbox.schema.addtable
ms.assetid: 3c0b1b30-795c-4240-91d6-890b8348014a
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 37b3207009e12b506f0ae80d9cdb0f1039442438
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253369"
---
# <a name="add-table-dialog-box-database-designer-visual-database-tools"></a>“添加表”对话框（数据库设计器）(Visual Database Tools)
  使用此对话框可以在数据库设计器中添加表。  
  
> [!NOTE]  
>  如果表是为复制发布的，则必须使用 Transact-SQL 语句 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) 或 SQL Server 管理对象 (SMO) 对架构进行更改。 使用表设计器或数据库关系图设计器更改架构后，会尝试删除并重新创建表。 由于您不能删除已发布的对象，因此架构更改将失败。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **“刷新”**  
 刷新表的列表以与数据库的当前状态匹配。  
  
 **“添加”**  
 添加所选的一个或多个表。  
  
> [!NOTE]  
>  如果希望将多个表添加到关系图中，可以将其全部选定，再单击“添加”。 或者，也可以双击要添加的每个表，然后在完成后单击“关闭”。  
  
 **关闭**  
 关闭对话框而不再添加表。  
  
## <a name="see-also"></a>请参阅  
 [向关系图中添加表 (Visual Database Tools)](visual-database-tools.md)  
  
  
