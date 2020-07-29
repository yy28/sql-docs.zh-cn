---
title: 绘制自反关系
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- drawing reflexive relationships
- reflexive relationships
- database diagrams [SQL Server], relationships
ms.assetid: e218363f-faec-46d5-9904-a537fbcc994d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: d87529fc1aebccecca90308475f6efeaf82f4a2f
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004952"
---
# <a name="draw-reflexive-relationships-visual-database-tools"></a>绘制自反关系 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
您可以创建自反关系，将一个表中的一列或多列与同一表中的另一列或多列相链接。 例如，假设 `employee` 表包含 `emp_id` 列和 `mgr_id` 列。 因为每个主管也是雇员，所以可以通过绘制该表与其自身的关系线将这两列相关。 此关系确保添加到表中的每个主管 ID 与一个现有雇员 ID 匹配。  
  
在创建关系之前，必须首先为表定义主键或唯一约束。 然后需要将主键列与匹配列相关。 一旦创建关系，匹配列即成为表的外键。  
  
### <a name="to-draw-a-reflexive-relationship"></a>绘制自反关系  
  
1.  在数据库关系图中，单击要与另一列相关联的数据库列的行选择器，并将指针拖出表外，直至有一个线条显示为止。  
  
2.  将该线条拖回所选的表。  
  
3.  释放鼠标按钮。 此时，将显示“表和列”  对话框。  
  
4.  选择外键列以及要与之建立关系的主键表和列。  
  
5.  选择“确定”  两次以创建关系。  
  
如果对表运行查询，则可使用自反关系创建自联接。 有关使用联接查询表的信息，请参阅 [使用联接进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)。  
  
## <a name="see-also"></a>另请参阅  
[使用联接进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
