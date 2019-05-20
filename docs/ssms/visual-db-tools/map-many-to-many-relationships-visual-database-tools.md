---
title: 映射多对多关系 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], many-to-many
- junction tables [SQL Server]
- many-to-many relationships [SQL Server]
- mapping many-to-many relationships [SQL Server]
- database diagrams [SQL Server], relationships
ms.assetid: 2977cf92-98b5-48b2-b0fd-8fbc7040f2b4
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6abe574ebfbe031d4a5ee1aa90698b566a4f84da
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65096656"
---
# <a name="map-many-to-many-relationships-visual-database-tools"></a>映射多对多关系 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
使用多对多关系，您可以将一个表中的每一行与另一个表中的多行相关，反之亦然。 例如，可以在 `authors` 表与 `titles` 表之间创建多对多关系，以将每位作者与其所有书籍相匹配并将每本书与其所有作者相匹配。 从上述任何一个表创建一对多关系都会错误地表示每本书只能有一位作者或者每位作者只能编写一本书。  
  
表与表之间的多对多关系通过联接表存储在数据库中。 联接表包含要相关的两个表的主键列。 然后，分别创建从每个表的主键列到联接表中的匹配列之间的关系。 在 pubs 数据库中， `titleauthor` 表为联接表。  
  
### <a name="to-create-a-many-to-many-relationship-between-tables"></a>在表与表之间创建多对多关系  
  
1.  在数据库关系图中，添加要在它们之间创建多对多关系的表。  
  
2.  右键单击关系图，然后从快捷菜单中选择“新建表”创建第三个表。 该表将成为联接表。  
  
3.  在“选择名称”对话框中，更改系统分配的表名。 例如，`titles` 表和 `authors` 表之间的联接表现在命名为 `titleauthors`。  
  
4.  将其他两个表中的主键列复制到联接表中。 与任何其他表一样，您可以向此表中添加其他列。  
  
5.  在联接表中，将主键设置为包含其他两个表中的所有主键列。 有关详细信息，请参阅[如何创建主键 (Visual Database Tools)](https://msdn.microsoft.com/85c623ca-4656-4d70-a9db-ee4d897cd214)。  
  
6.  分别定义每个主表与联接表之间的一对多关系。 联接表应位于您所创建的这两个关系的“多”方。 有关详细信息，请参阅[如何在表之间创建关系 (Visual Database Tools)](https://msdn.microsoft.com/867a54b8-5be4-46e6-9702-49ae6dabf67c)。  
  
    > [!NOTE]  
    > 在数据库关系图中创建联接表并不会将数据从相关表插入联接表中。 有关将数据插入表的信息，请参阅[创建插入结果查询 (Visual Database Tools)](../../ssms/visual-db-tools/create-insert-results-queries-visual-database-tools.md)。  
  
## <a name="see-also"></a>另请参阅  
[使用数据库关系图 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
