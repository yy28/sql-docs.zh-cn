---
title: 在多个列上联接表 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiple column joins
- joins [SQL Server], multiple columns
ms.assetid: 56a158bc-a42a-4b78-baad-4721d2d22cd3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fa18294f62eed2a412d3abbb5bb9d740a4364499
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685175"
---
# <a name="join-tables-on-multiple-columns-visual-database-tools"></a>在多个列上联接表 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
您可以使用多个列来联接表。 即可以创建这样的一个查询，仅当来自两个表中的行都满足多个条件时才与该查询匹配。 如果数据库包含的关系将一个表中的多个外键列与另一个表中的多列主键匹配，则可使用此关系创建多列联接。 有关详细信息，请参阅[自动联接表 (Visual Database Tools)](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md)。  
  
即使数据库不包含多列外键关系，也可手动创建多列联接。  
  
### <a name="to-manually-create-a-multicolumn-join"></a>手动创建多列联接  
  
1.  将要联接的表添加到 [“关系图”窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) 中。  
  
2.  拖动第一个表窗口中的第一个联接列的名称，并将其放到第二个表窗口的相关列上。 不能基于 text、ntext 或 image 列建立联接。  
  
    > [!NOTE]  
    > 通常，联接列必须具有相同（或兼容）的数据类型。 例如，如果第一个表中的联接列是日期，则必须将其与第二个表中的日期列相关。 另一方面，如果第一个联接列是整数，则相关联接列也必须是整数数据类型，但它的大小可以不同。 但是，在某些情况下，隐式数据类型转换可以成功地联接看起来不兼容的列。  
    >   
    > [查询和视图设计器](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 不检查要用来创建联接的列的数据类型，但当执行查询时，如果数据类型不兼容，数据库将显示错误。  
  
3.  拖动第一个表窗口中的第二个联接列的名称，并将其放到第二个表窗口中的相关列上。  
  
4.  对于两个表中的其他每个联接列对，重复第 3 步。  
  
5.  运行查询。  
  
## <a name="see-also"></a>另请参阅  
[使用联接进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
