---
title: 绘制自反关系 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- drawing reflexive relationships
- reflexive relationships
- database diagrams [SQL Server], relationships
ms.assetid: e218363f-faec-46d5-9904-a537fbcc994d
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 08e3d4d09c08abd5453322430f6d6ccfc8456a1d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018319"
---
# <a name="draw-reflexive-relationships-visual-database-tools"></a>绘制自反关系 (Visual Database Tools)
  您可以创建自反关系，将一个表中的一列或多列与同一表中的另一列或多列相链接。 例如，假设 `employee` 表包含 `emp_id` 列和 `mgr_id` 列。 因为每个主管也是雇员，所以可以通过绘制该表与其自身的关系线将这两列相关。 此关系确保添加到表中的每个主管 ID 与一个现有雇员 ID 匹配。  
  
 在创建关系之前，必须首先为表定义主键或唯一约束。 然后需要将主键列与匹配列相关。 一旦创建关系，匹配列即成为表的外键。  
  
### <a name="to-draw-a-reflexive-relationship"></a>绘制自反关系  
  
1.  在数据库关系图中，单击要与另一列相关联的数据库列的行选择器，并将指针拖出表外，直至有一个线条显示为止。  
  
2.  将该线条拖回所选的表。  
  
3.  释放鼠标按钮。 此时，将显示“表和列”对话框。  
  
4.  选择外键列以及要与之建立关系的主键表和列。  
  
5.  选择“确定”两次以创建关系。  
  
 如果对表运行查询，则可使用自反关系创建自联接。 有关使用联接查询表的信息，请参阅 [使用联接进行查询 (Visual Database Tools)](visual-database-tools.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用联接进行查询 (Visual Database Tools)](visual-database-tools.md)  
  
  