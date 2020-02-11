---
title: 数据库演化问题 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], multuser database changes
- database evolution [SQL Server]
ms.assetid: 1ed6ae10-d212-4ec2-8569-1b94ab1cba6d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d3a1f10ae77061983a5cf64ddd5a3462bb4be49b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63035586"
---
# <a name="issues-of-database-evolution-visual-database-tools"></a>数据库演化问题 (Visual Database Tools)
  如果更改已部署的数据库的结构，则必须特别留意更改应与现有的数据和数据库结构兼容。 当进行以下修改时，可能需要采取特殊步骤：  
  
-   **添加约束**如果添加约束，数据库可能已经包含不满足该约束的数据。 当尝试保存新约束时，[“保存后通知”对话框 (Visual Database Tools)](visual-database-tools.md) 将通知你数据库服务器无法创建该约束。 若要强制数据库接受新约束，可以清除“在创建时检查现有数据”**** 复选框。  
  
-   **添加关系**如果添加关系，则数据库可能已包含外键表中的行，而主键表中没有对应的行。 即现有数据可能不满足引用完整性。 尝试保存新关系时，[“保存后通知”对话框 (Visual Database Tools)](visual-database-tools.md) 将通知你数据库服务器无法保存修改过的外键表。 若要强制数据库接受修改，可以清除“在创建时检查现有数据”**** 复选框。  
  
-   **修改构成索引视图的表**如果修改了分配给 Microsoft SQL Server 索引视图的表，该视图的索引将丢失。 有关重新创建索引的信息，请参阅 SQL Server 联机丛书。  
  
-   **删除对象**如果删除某个对象（例如列、表或视图），请首先检查以确保该对象不是由数据库中的其他对象引用的。  
  
 无论如何更改数据库设计，都应保留更改的历史记录。 可以通过保留对成品数据库进行的所有修改的 SQL 脚本来保留所做更改。  
  
## <a name="see-also"></a>另请参阅  
 [Unique 约束和 Check 约束](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [多用户环境 &#40;Visual Database Tools&#41;](multiuser-environments-visual-database-tools.md)  
  
  
