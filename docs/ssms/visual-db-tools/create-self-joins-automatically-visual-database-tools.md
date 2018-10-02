---
title: 自动创建自联接 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- self-joins
- joins [SQL Server], self
ms.assetid: f9ec90e8-3aad-415c-a5c4-8dfa9540e37f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0f1d7bdeca1202eb46bf2926d2ddc86855bd5f71
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47652506"
---
# <a name="create-self-joins-automatically-visual-database-tools"></a>自动创建自联接 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
如果表在数据库中有自反关系，则可自动将其与自身联接。  
  
### <a name="to-create-a-self-join-automatically"></a>自动创建自联接  
  
1.  将要处理的表添加到 [“关系图”窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) 中。  
  
2.  再次添加同一表，以便“关系图”窗格显示同一表两次。  
  
    [查询和视图设计器](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 将通过为表名添加一个顺序号来为第二个实例分配别名。 此外，查询和视图设计器还会在表示该表参与查询的两种不同方式的两个矩形之间创建联接线。  
  
## <a name="see-also"></a>另请参阅  
[使用联接进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
